---
tags:
  - CI_CD
---
In DevOps geht es darum den Entwicklern (Dev) und dem IT-Betriebsteam (Ops) die Zusammenarbeit zu erleichtern. Die Ziele/Grundprinzipien sind folgende:

# Automatisierung

Die Automatisierung steht im Fokus, da hier Fehler minimiert werden können. Hier stehen im Fokus Abläufe wie:
- Bauen der Software
- Tests durchführen
- Bereitstellung
Die Ablaufe werden durch die sogenannte CI/CD Pipeline ermöglicht.

## CI

In Continuous Integration (CI) geht es um das regelmäßige Tracking von Code Änderungen und die Integration dieser um Fehler frühzeitig zu erkennen.

Realisiert wird dies meist durch eine Kombination von einem Version Control Systeme wie [[Git]] und einem Remote Repository wie GitHub oder Bitbucket welche Änderungen tracken und diese in die CI-Pipeline bringen. 

Die CI-Pipeline führt nun automatisch das Bauen und Testen der Software durch und gibt dem Entwickler Feedback zu seinem Code.

## CD

In Continuous Delivery / Continuous Deployment (CD) geht es um das ständige Updaten der Software wenn diese durch die CI-Pipeline als stabil befunden wird.

Hierbei wird das Update zunächst in eine Testumgebung eingeführt, welche der Produktionsumgebung stark ähnelt, um hier weiter testen zu können.

Nachdem hier alles als stabil empfunden wird, kann das Update in die Produktion überführt werden , was meist aber durch eine menschliche Genehmigung erlaubt werden muss.

# Zusammenarbeit

DevOps strebt aber auch an Zusammenarbeit weiter zu fördern. Während die CI/CD Pipeline hier viel Beiträgt ist sie nicht der Kernaspekt. DevOps strebt an, auch außerhalb der CI/CD Pipeline den Austausch zwischen den Entwicklern und dem Betriebsteam / Endnutzern zu fördern.

Beispielsweise gibt es hier regelmäßige Treffen um sich Auszutauschen über den aktuellen Stand oder Pläne des Projektes. Um diese regelmäßige Kommunikation zu fördern werden Rahmenwerke wie Scrum verwendet.

