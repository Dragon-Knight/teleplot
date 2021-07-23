# Teleplot

A ridiculously simple tool to plot telemetry data from a running program.

![](preview.jpg)

`echo "myData:4|g" | nc -u -w0 127.0.0.1 47269`

# Start the server

## Using node
```bash
cd server
npm i
node main.js
```

Open your navigator at [127.0.0.1:8080](127.0.0.1:8080)

## Using docker
```bash
cd server
docker build -t teleplot .
docker run -d -p 8080:8080 -p 47269:47269/udp teleplot
```

Open your navigator at [127.0.0.1:8080](127.0.0.1:8080)

## Using docker-compose
```bash
cd server
docker-compose build
docker-compose up
```

Open your navigator at [127.0.0.1:8080](127.0.0.1:8080)

# Publish telemetry

## Bash

```bash
echo "myValue:1234|g" | nc -u -w0 127.0.0.1 47269
```

## C++

Copy `Teleplot.h` in your project and use its object.
```cpp
#include <math.h>
#include "Teleplot.h"
Teleplot teleplot("127.0.0.1");

int main(int argc, char* argv[])
{
    for(float i=0;i<1000;i+=0.1)
    {
        teleplot.update("sin", sin(i));
        teleplot.update("cos", cos(i));
        teleplot.update("tan", tan(i));
        usleep(10000);
    }
    return 0;
}
```