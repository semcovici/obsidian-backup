In the time series analysis, we assume that the [[Stochastic Process]] has the property of stationarity.

**Definition:**  Stationary Stochastic Process are  those that the probabilistic characteristics doesn't change over time

The stationary series have the same probability distribution for each observation. However, this definition is extremely restrictive and difficulty to verify in the real world.  Because of that, there are the definitions of weak stationarity and strong stationarity

![[../files/Pasted image 20240603153151.png]]

### Strong stationarity 

* The density joint probability function is time invariant
* The individual distributions are  equal for all t



### Weak Stationarity

* The mean, variance and covariance of the series are constants over time
	* $E(Y_t) = \mu$
	* $\text{var}(Y_t) = E[(Y_t - E(Y_t))^2] = \gamma_0 < \infty$
	* $\text{cov}(Y_{t}, Y_{t-k}) = E[(Y_{t} - E(Y_{t}))(Y_{t-k} - E(Y_{t-k}))] = \gamma_k; k=1,2,…,T-1.$ 
* this condition is less restrictive and possible to reach in economics data

