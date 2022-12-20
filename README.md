# Emulator for Caliptra 

This repository contains code for creating an emulator for the Caliptra hardware.

## Peripheral Emulation

### Mailbox 

#### Class Diagram
```plantuml
@startuml mb_class_diagram
Bus <|-- MailboxIface

class MailboxIface {
  == Event triggers ==
  +read_lock()
  +write_cmd()
  +write_data_len()
  +write_exec()
 }

enum Events {
  LockRead,
  CmdWrite,
  DataLenWrite
  ExecWrite
}

class StateMachine <<Singleton>> {
  +process_event()
}

class Context {
  +enqueue()
  +dequeue()
  -ring_buffer
}

MailboxIface --> StateMachine
StateMachine o-- Context

@enduml

```

#### Mailbox State Machine
The UML state diagram depicted below represents the behavior of the mailbox state machine. The notation follows the UML conventions:

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



Some more markdown.
