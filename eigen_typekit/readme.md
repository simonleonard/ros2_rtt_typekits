# Eigen typekit

to load the typekits using the ros2 build system, we need the ```rtt_ros2``` package, e.g. in rttlua

```
require("rttlib")
tc = rtt.getTC()
depl = tc:getPeer("Deployer")
depl:import("rtt_ros2")
rtt.provides("ros"):import("eigen_typekit")
vec=rtt.Variable("eigen_vector")
vec:resize(3)
print(vec)
print(vec[0]) -- these type are 0-indexed !!

```

