# Which 命令总结

## 基本流程

```text
                                                                                                                                     
                                                                                                                                     
                                                                                                                                     
                                                                                                                                     
                                                                                                                                     
                                                                                                                                     
                                                                       ┌─────────┐                                                   
                                                                       │  Begin  │                                                   
                                                                       └─────────┘                                                   
                                                                            │                                                        
                                                                            ▼                                                        
                       ┌───────────────┐     option -h     ┌────────────────────────────────┐                                        
                       │  Print usage  │◀────────is ───────│  Parse command line arguments  │                                        
                       └───────────────┘     specified     └────────────────────────────────┘                                        
                               │                                            │                                                        
                               ▼                                            ▼                                                        
                    ┌─────────────────────┐            ┌─────────────────────────────────────────┐                                   
                    │  Exit and return 0  │            │  Get $filename and status of option -a  │                                   
                    └─────────────────────┘            └─────────────────────────────────────────┘                                   
                               │                                            │                                                        
                               │                                            ▼                                                        
                               │                          ┌──────────────────────────────────┐                                       
                               │                          │  Get $PATH environment variable  │                                       
                               │                          └──────────────────────────────────┘                                       
                               │                                            │                                                        
                               │                                            ▼                                                        
                               │               ┌─────────────────────────────────────────────────────────┐                           
                               │               │  Split $PATH by separator and put them into $path_list  │                           
                               │               └─────────────────────────────────────────────────────────┘                           
                               │                                            │                                                        
                               │                                            ▼                                                        
                               │                 ┌─▶┌───────────────────────────────────────────────┐────────────────────┐           
                               │                 │  │  Pop the first item from $path_list as $path  │                    │           
                               │                 │  └───────────────────────────────────────────────┘◀─┐                 │           
                               │                 │  ▲                       │                          │                 │           
                               │                 │  │                       ▼                          │                 ▼           
                               │                 │  no ┌─────────────────────────────────────────┐     │      ┌─────────────────────┐
                               │                 │  └──│  Check $filename if exists under $path  │     │      │  Exit and return 1  │
                               │                 │     └─────────────────────────────────────────┘     │      └─────────────────────┘
                               │                 │                          │                          │                 │           
                               │                 no                        yes                    option -a              │           
                               │                 │                          │                         is                 │           
                               │                 │                          ▼                     specified              │           
                               │                 │       ┌────────────────────────────────────┐        │                 │           
                               │                 └───────│  Check $filename if is executable  │        │                 │           
                               │                         └────────────────────────────────────┘        │                 │           
                               │                                            │                          │                 │           
                               │                                           yes                         │                 │           
                               │                                            │                          │                 │           
                               │                                            ▼                          │                 │           
                               │                                 ┌─────────────────────┐               │                 │           
                               │                                 │     Print $path     │───────────────┘                 │           
                               │                                 └─────────────────────┘                                 │           
                               │                                            │                                            │           
                               │                                            ▼                                            │           
                               │                                 ┌─────────────────────┐                                 │           
                               │                                 │  Exit and return 0  │                                 │           
                               │                                 └─────────────────────┘                                 │           
                               │                                            │                                            │           
                               │                                            ▼                                            │           
                               │                                        ┌───────┐                                        │           
                               └───────────────────────────────────────▶│  End  │◀───────────────────────────────────────┘           
                                                                        └───────┘                                                    
```

