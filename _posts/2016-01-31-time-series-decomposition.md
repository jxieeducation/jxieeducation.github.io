---
layout: post
category : tutorial
tags: visualization, anomalydetection
tagline: "Time series decomposition"
excerpt: Time series datasets have so many applications, from seasonal analysis to anomaly detection. Today, I am going to use the Nottingham temperature dataset as an example. My goal is provide a naive and intuitive explanation of time series decomposition.

---



### Nottingham dataset

Time series datasets have so many applications, from seasonal analysis to anomaly detection. Today, I am going to use the [Nottingham temperature dataset](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/nottem.html) (nottem for short) as an example. My goal is provide a naive and intuitive explanation of time series decomposition.

![nottem raw]({{site.imgrepo}}/nottem_raw.png)

### Seasonal

We can think of a time series, $X_t$, as 3 components: seasonal, trend, residual. $X_t = S_t + T_t + e_t$

The seasonal component is responsible for the sinusoidal behavior. For instance, temperature always goes up in the summer and down in the winter because of the seasonal component. 

We can think of the seasonal component as a function of time. $S(t) = \alpha * sin(2\pi t) + \beta * cos(2\pi t)$

`plot(lnottem)`

`lines(t, lm(lnottem~sin.t + cos.t)$fit, col="green")`

![nottem seasonal]({{site.imgrepo}}/nottem_seasonal.png)

### Trend

The trend component ($T_t$) is an overall progression of the temperature over time. For instance, because of global warming, there is an overall trend for the temperature to increase in the 20th century.

We can obtain a function of the trend by fitting a line through the data. 

`t_2 <- t^2`

`t_3 <- t^3`

`plot(lnottem)`

`lines(t, lm(lnottem~t + t_2 + t_3)$fit, col="blue")`

![nottem trend]({{site.imgrepo}}/nottem_trend.png)

### Residual

The residual component ($e_t$) is a variable for us to explain what we can't understand through the seasonal and trend components.

$e_t = X_t - S_t - T_t$

Here's how it looks with the seasonal and trend component.

`lines(t, lm(lnottem~t + t_2 + t_3 + sin.t + cos.t)$fit, col="purple")`

![nottem seasonal trend]({{site.imgrepo}}/nottem_seasonal_trend.png)

And here's the residual.

`plot(t, lnottem - lm(lnottem~t + t_2 + t_3 + sin.t + cos.t)$fit + rep(mean(lnottem), length(t)), col="red", type="l")`

![nottem residual]({{site.imgrepo}}/nottem_residual.png)

### Conclusion

![nottem residual]({{site.imgrepo}}/nottem_stl.png)

By decomposing times series data into 3 components ($S_t, T_t, e_t$), we can understand the time series better. Techniques such as time series anomaly detection and forecasting.

