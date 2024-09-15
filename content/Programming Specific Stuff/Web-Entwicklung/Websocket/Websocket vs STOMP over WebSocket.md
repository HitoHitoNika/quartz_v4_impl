## Kurzabriss: Was ist Websocket

- TCP basiertes Protokoll
- Ziel: Bidirektionale Echtzeit Verbindung zwischen Webanwendung und Server

#### Websocket Handshake

![[Pasted image 20240913212041.png]]

#### Warum nicht einfach HTTP?

Im Gegensatz zu HTTP Requests bleibt die Verbindung nicht nur bestehen, sondern Nachrichten können von beiden Seiten aus kommen. Dementsprechend kann auch von beiden Seiten reagiert werden!

![[Pasted image 20240913212126.png]]

## Was ist STOMP?

STOMP (Simple/Streaming Text Orientated Messaging Protocol) ähnelt im ersten Moment eher MQTT. Man hat ein Publish / Subscribe verfahren über welches Nachrichten ausgetauscht werden.

![[Pasted image 20240913213447.png]]

Auch wenn der Name im ersten Moment der Name vermuten lässt das STOMP eher ein Konkurrent zu MQTT und Websocket ist, wird STOMP häufig eben nicht allein stehend verwendet sondern eher über die Websocket-API der Browser genutzt. Man kann also sagen das STOMP und Websocket eine ähnliche Beziehung führen wie HTTP und TCP.

## Gibt es Vor- und Nachteile?

Kurzgefasst: Jain ?

STOMP wird nachgesagt das es einem Entwickler "viel" Arbeit abnimmt. Das hängt aber sehr stark davon ab was man erreichen möchte und ist auch nur bedingt ein Vorteil.

### Unterscheidung der Nutzer

Unterscheidung der Nutzer über STOMP ist wesentlich einfacher, da das ganze über die Topics passiert. In Websocket müsste man Beispielsweise beim Handshake in der URL Query Params mitgeben, diese dann im Backend verarbeiten und zu einer Session mappen. 

Hier konkrete Code Beispiele für das Backend
##### Websocket

**WebSocketConfig**

Hier bestimmen wir welche Klasse sich um die Verbindungen kümmert und auf diese reagiert.

```java
@Configuration
@EnableWebSocket
public class WebSocketConfig implements WebSocketConfigurer {

    @Override
    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
        registry.addHandler(new MyWebSocketHandler(), "/ws")
                .setAllowedOrigins("*");
    }
}

```

**MyWebSocketHandler**

Hier steuern wir was passiert wenn:
- Ein Nutzer sich verbindet
- Ein Nutzer die Verbindung schließt
- Eine Message erhalten wird
- Eine Message versandt werden soll

```java
public class MyWebSocketHandler extends TextWebSocketHandler {

    // Map zur Speicherung der WebSocketSession und der zugehörigen Nutzerinformationen (z.B. Nutzer-ID)
    private final Map<WebSocketSession, String> sessions = new ConcurrentHashMap<>();

    @Override
    public void afterConnectionEstablished(WebSocketSession session) throws Exception {
        // Beispiel: Nutzer-ID als Query-Parameter empfangen und speichern
        String userId = session.getUri().getQuery().split("=")[1]; // Annahme: URL enthält ?userId=123
        sessions.put(session, userId);
        System.out.println("User connected: " + userId);
        session.sendMessage(new TextMessage("Welcome, user " + userId + "! You are now connected."));
    }

    @Override
    public void afterConnectionClosed(WebSocketSession session, org.springframework.web.socket.CloseStatus status) throws Exception {
        // Session entfernen, wenn der Nutzer die Verbindung schließt
        String userId = sessions.remove(session);
        System.out.println("User disconnected: " + userId);
    }

    @Override
    public void handleTextMessage(WebSocketSession session, TextMessage message) throws IOException {
        String payload = message.getPayload();
        String userId = sessions.get(session);  // Hole die Nutzer-ID zu der aktuellen Session
        System.out.println("Received from user " + userId + ": " + payload);

        // Beispiel: Nachricht nur an Nutzer mit einer bestimmten ID senden (z.B. userId = "123")
        for (Map.Entry<WebSocketSession, String> entry : sessions.entrySet()) {
            if ("123".equals(entry.getValue())) {  // Nur Nutzer mit ID "123"
                WebSocketSession s = entry.getKey();
                if (s.isOpen()) {
                    s.sendMessage(new TextMessage("Private message to user 123: " + payload));
                }
            }
        }
    }
}

```

Ganz wichtig ist hier anzumerken: Wir müssen uns darum kümmern das wir die Nutzer unterscheiden können! Wenn wir dies nicht machen haben wir nur die Session vorliegen, die zwar auf einen Nutzer verweist ABER nur mitgegeben wird wenn wir bspw eine Nachricht von diesem erhalten. Bedeutet wir könnten nicht eine Nachricht die per REST kam ohne weiteres an Nutzer xyz weiterleiten.
##### STOMP

**WebSocketConfig**

Hier konfigurieren wir:
- Den Präfix der Topics
- Die Topic die abonniert werden kann (lässt sich nach hinten erweitern)
- Einen Endpunkt zum registrieren der Verbindung

```java
@Configuration  
@EnableWebSocketMessageBroker  
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {  
  
    @Override  
    public void configureMessageBroker(MessageBrokerRegistry config) {  
        config.enableSimpleBroker("/command");  
        config.setApplicationDestinationPrefixes("/app");  
    }  
  
    @Override  
    public void registerStompEndpoints(StompEndpointRegistry registry) {  
        registry.addEndpoint("/registry")  
                .setAllowedOrigins("http://localhost:4200");  
    }  
}
```


**MessageController**

Der MessageController stellt Endpunkte mit der Annotation @MessageMapping. Diese dient nur dazu Nachrichten von außen entgegen zunehmen und auf diese dann zu reagieren. Man kann also sagen, das sind die Topics auf die das Backend am lauschen ist.

```java
@Controller  
public class MessageController {  
  
    SimpMessagingTemplate messagingTemplate;  
    Logger logger;  
  
    @Autowired  
    MessageController(SimpMessagingTemplate messagingTemplate){  
        this.messagingTemplate = messagingTemplate;  
        this.logger = LoggerFactory.getLogger(MessageController.class);  
    }  
  
    @MessageMapping("/adminCommand/{team}")  
    public void sendCommand(String command, @DestinationVariable("team") String team) {  
        logger.info("Der Command: {} wird an das Team: {} weitergeleitet",command,team);  
        messagingTemplate.convertAndSend("/command/"+team, command);  
    }  

	//Diese Methode könnte von einem REST-Controller verwendet werden um Nachrichten zu verschicken
    public void sendCommand(CommandDTO commandDTO){  
        logger.info("CommandDTO: {}", commandDTO);  
        messagingTemplate.convertAndSend("/command/"+commandDTO.team, commandDTO.command.getCommand());  
    }  
}
```

Hier wird der Vorteile der Topics deutlich. Wir können einfach eine Nachricht an ".../adminCommand/ATeam" schicken und können uns hiermit die Topic zusammen basteln bspw ".../command/ATeam". Wir müssen uns keine Nutzer merken da diese selber entscheiden für was sie sich interessieren.

### Feinheit

Wie man an den oberen Beispiel auch sehen kann, kann man mit einer puren Websocket Verbindung viel besser und genauer bestimmen was passieren soll, da man diese selber Implementieren muss. STOMP nimmt einem diese Arbeit, kommt dadurch aber mit seinen eigenen Regeln.

### Acknowledgements

STOMP hat in der Spezifikation einige Sachen vorgeschrieben, unter anderem das es eine ACK Meldung auf jede Nachricht geben muss. Während man hier argumentieren kann, dass wir hierdurch gewissen Overhead haben, da der Websocket Standard sowas nicht direkt vorsieht, ist es in einige Fällen wichtig zu wissen das die Nachricht ankam.


## Fazit

Insgesamt lässt sich schwer sagen, welches die _beste_ Lösung ist. **STOMP** bietet auf den ersten Blick viele Vorteile, wobei **WebSocket** hingegen durch seine maximale Flexibilität und Kontrolle punkten kann. Für einfache Echtzeitanwendungen ohne zusätzliche Protokolle ermöglicht es eine sehr feingranulare Anpassung, mit der **STOMP** per Design nicht mithalten kann.