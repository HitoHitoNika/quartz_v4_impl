
## Was ist der Encryption Service

Der Encryption Service ist für alles was die Verschlüsselung angeht verantwortlich.

Er generiert ein Schlüssel basierend auf dem Passwort des Users und verschlüsselt sämtliche Daten des Users mit diesem.

## UML

```plantuml
@startuml

class EncryptionService {
  -ALGORITHM: String
  -ITERATIONS: int
  -KEY_LENGTH: int
  -SALT: byte[]
  -secretKey: SecretKey
  +EncryptionService(masterPassword: String)
  +getSecretKey(): SecretKey
  +encryptString(plainText: String): String
  +decryptString(encryptedText: String): String
}

@enduml
```
