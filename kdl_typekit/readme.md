# KDL typekit

to load the typekits using the ros2 build system, we need the ```rtt_ros2``` package, e.g. in rttlua

```
require("rttlib")
tc = rtt.getTC()
depl = tc:getPeer("Deployer")
depl:import("rtt_ros2")
rtt.provides("ros"):import("kdl_typekit")
t=rtt.Variable("KDL.Frame")
```
some examples of usage in the (lua cookbook)[https://www.orocos.org/wiki/LuaCookBook.html]
