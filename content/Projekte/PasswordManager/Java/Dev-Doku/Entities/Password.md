Back to [[Table of Contents]]
## Was macht die Password Entity

Die Password Klasse dient dazu alle nötigen Daten des jeweiligen Daten in einem Objekt festzuhalten und den Umgang mit diesem zu erleichtern

## UML

```plantuml

@startuml

class Password {
  -value: String
  -username: String
  -plattform: String
  -uuid: UUID
  +Password(value: String, username: String, plattform: String, uuid: UUID)
  +getValue(): String
  +setValue(value: String)
  +getUsername(): String
  +setUsername(username: String)
  +getPlattform(): String
  +setPlattform(plattform: String)
  +getUuid(): UUID
  +setUuid(uuid: UUID)
  +toString(): String
}

@enduml
```