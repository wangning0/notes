# Functional Programming Learning

## Attention

* pure function

* higher-order function

* Don't use iterate (eg: for、while etc)

  > we should use map、reduce、filter etc
  
* Avoid mutability

    ```
    // -> bad
    var rooms = ['h1', 'h2', 'h3'];
    rooms[2] = 'h4';
    rooms;
    // => ['h1', 'h2', 'h4']
    
    // -> good
    
    var rooms = ['', '', '']
    ```

