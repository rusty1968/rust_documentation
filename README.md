Regular **Markdown** here.

```
@startuml mb_state_diagram

[*] --> Idle

Idle -> RdyForCmd : Ev_LockRd [unlocked] / lock 
RdyForCmd --> RdyForDlen : Ev_DlenWr
RdyForDlen --> RdyForData : Ev_DataInWr / enqueue
RdyForData --> Exec : Ev_ExecWr
Exec --> Exec : Ev_DataOutRd / dequeue
Exec --> Idle : Ev_ExecWr

@enduml
```

![](firstDiagram.svg)

Some more markdown.
