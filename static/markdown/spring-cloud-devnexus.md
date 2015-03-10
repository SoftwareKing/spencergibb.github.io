## Cloud Native Apps
## with Spring Cloud

<style>img[alt=spring-cloud] { width: 40%; float: right; border: 0px solid #fff;}</style>

![spring-cloud](/images/spring-cloud.png)

Spencer Gibb<br>
twitter: [@spencerbgibb](http://twitter.com/spencerbgibb)<br>
email: sgibb@pivotal.io

Dave Syer<br>
twitter: [@david_syer](http://twitter.com/david_syer)<br>
email: dsyer@pivotal.io



## ![pivotal](/images/pivotal_logo.png)

<style>img[alt=spring_io] { width: 40%; }</style>
<style>img[alt=gemfire] { width: 80%; }</style>
<style>img[alt=greenplum] { width: 40%; }</style>
<style>img[alt=tomcat] { width: 40%; }</style>

|               |               |       |
| ------------- |:-------------:| -----:|
| ![cf_logo](/images/cf_logo.png) | ![spring_io](/images/spring-io.png) | ![rabbitmq](/images/rabbitmq.png) |
| ![gemfire](/images/gemfire.png)  | ![greenplum](/images/greenplum.jpg) | ![pivotal_labs](/images/pivotal_labs_logo.png) |
| ![redis](/images/redis.png) | ![tomcat](/images/tomcat_logo.png) | ![bigtop](/images/bigtop.png) |


## Cloud Native

* Distributed
* Automated
* Organizational
* Anti-fragile

<blockquote cite="https://twitter.com/spencerbgibb/status/566399494154371072">I like 'cloud native' better than microservice. I think its more descriptive and doesn't have the awkwardness of having 'micro" in the name.</blockquote>



## Cloud Native with Spring Boot

It needs to be super easy to implement and update a service:

```
@RestController
class ThisWillActuallyRun {
  @RequestMapping("/")
  String home() {
    Hello World!
  }
}
```



### Example Distributed System: Minified

<style>img[alt=myfeed-blank] { width: 70%; }</style>

![myfeed-blank](/images/myfeed_arch_blank.svg)



### No Man (Microservice) is an Island

> It's excellent to be able to implement a microservice really easily
> (Spring Boot), but building a system that way surfaces
> "non-functional" requirements that you otherwise didn't have.

There are laws of physics that make some problems unsolvable
(consistency, latency), but brittleness and manageability can be
addressed with *generic*, *boiler plate* patterns.



## Emergent features of cloud native systems

Coordination of distributed systems leads to boiler plate patterns

* Distributed/versioned configuration
* Service registration and discovery
* Routing
* Service-to-service calls
* Load balancing
* Circuit Breaker
* Asynchronous
* Distributed messaging



## Spring IO Platform

![spring-io-tree](/images/spring-io-tree.png)



### Example: Coordination Boiler Plate

<style>img[alt=myfeed-system] { width: 70%; }</style>

![myfeed-system](/images/myfeed_arch_system.svg)



## Netflix OSS

<style>img[alt=Netflix_logo] { width: 60%; float: right; }</style>

![Netflix_logo](/images/Netflix_logo.svg)

* Eureka
* Hystrix & Turbine
* Ribbon
* Feign
* Zuul
* Archaius

* Curator
* Asgaard
* ...



### Example: Spring Cloud and Netflix

<style>img[alt=myfeed] { width: 70%; }</style>

![myfeed](/images/myfeed_arch.svg)



## Configuration Server

<style>img[alt=gears] { width: 40%; float: right; }</style>

![gears](/images/gears.svg)

* Pluggable source
* Git implementation
  * Per service repos
* SVN implementation
* Versioned
* Rollback-able
* Configuration client <br>auto-configured via starter



## Discovery: Eureka

<style>img[alt=eureka] { width: 30%; float: right; }</style>

![eureka](/images/eureka.png)

* Service Registration Server
* Highly Available
* In AWS terms, multi Availability<br>Zone and Region aware

http://techblog.netflix.com/2012/09/eureka.html



## Client Side Load-balancing: Ribbon

<style>img[alt=ribbon] { width: 30%; float: right; }</style>

![ribbon](/images/ribbon.png)

* Client side load balancer
* Pluggable
* Round robin, random,<br>weighted response time

http://techblog.netflix.com/2013/01/announcing-ribbon-tying-netflix-mid.html



## Circuit Breaker: Hystrix

<style>img[alt=hystrix-logo] { float: right; }</style>

![hystrix-logo](/images/hystrix-logo.png)

* latency and fault tolerance
* isolates access to other services
* stops cascading failures
* enables resilience
* circuit breaker pattern
* dashboard

http://techblog.netflix.com/2012/11/hystrix.html


## Hystrix 

<style>img[alt=hystrix] { width: 92%; }</style>

![hystrix](/images/HystrixGraph.svg)


## Hystrix Fallback

<style>img[alt=hystrix] { width: 92%; }</style>

![hystrix](/images/HystrixFallback.svg)



## Circuit Breaker Metrics

* Via actuator `/metrics`
* Server side event stream `/hystrix.stream`
  * also via rabbitmq
* Dashboard app via `@EnableHystrixDashboard`



## Rx Java

<style>img[alt=rx-logo] { width: 15%; float: right; }</style>

![rx-logo](/images/Rx_Logo_M.png)

* Reactive: push vs. pull
* Functional
* Composable
* Return `Observable` from Spring MVC<br>Controller (soon)
* API Gateway combining services


## Rx Java Example
```
public static void hello(String... names) {
    Observable.from(names).subscribe(s -> {
            System.out.println("Hello " + s + "!");
    });
}
```

Sample functions:
* map
* flatMap
* zip
* take
* merge
* 350+ operators!

http://techblog.netflix.com/2013/02/rxjava-netflix-api.html<br>
https://github.com/ReactiveX/RxJava<br>
http://reactivex.io



## Routing: Zuul

<style>img[alt=zuul] { width:30%; float: right; }</style>

![zuul](/images/zuul.png)

* JVM based router and filter
* Similar routing role as httpd,<br>nginx, or CF go router
* Fully programmable rules and filters
* Groovy
* Java
* any JVM language

http://techblog.netflix.com/2013/06/announcing-zuul-edge-service-in-cloud.html


## How Netflix uses Zuul
* Authentication
* Insights
* Stress Testing
* Canary Testing
* Dynamic Routing
* Service Migration
* Load Shedding
* Security
* Static Response handling
* Active/Active traffic management



## Spring Cloud Security

Enable Single Sign On (SSO) with an OAuth2 provider declared in external properties.

```
@EnableOAuth2Sso
```
Enable security using OAuth2 access tokens

```
@EnableOAuth2Resource
```



## Spring Cloud Bus

* Distributed actuator
* `/bus/env` and `/bus/refresh` actuator endpoints
* uses Spring Messaging and Spring Integration



## No soup for you!

![nojava](/images/nojava.png)



## Spring Cloud Sidecar

<style>img[alt=sidecar] { width: 50%; float: right; }</style>

![sidecar](/images/Vespa_sidecar.png)

* For you non-java apps
* Modeled after Netflix Prana
* Built in zuul proxy

http://techblog.netflix.com/2014/11/prana-sidecar-for-your-netflix-paas.html



## Spring Cloud Future

_Previews, experiments or ideas_ (ie: **no guarantees!**)

* Distributed Locks, Leader election
* Consul: Config, Discovery, Bus, Locks
* Zookeeper or etcd: Locks, Leader Election, Discovery, Config
* Zipkin for distributed tracing
* Moar Bus! Moar Messaging!




## Links

* [http://github.com/spring-cloud](http://github.com/spring-cloud)
* [http://github.com/spring-cloud-samples](http://github.com/spring-cloud-samples)
* [http://blog.spring.io](http://blog.spring.io)
* [http://presos.dsyer.com/decks/spring-cloud.html](http://presos.dsyer.com/decks/spring-cloud.html)
* Twitter: [@spencerbgibb](http://twitter.com/spencerbgibb), [@david_syer](http://twitter.com/david_syer)
* Email: sgibb@pivotal.io, dsyer@pivotal.io



## Notes

* [CD with CF](https://speakerdeck.com/mstine/architecting-for-continuous-delivery-microservices-with-pivotal-cf-and-spring-cloud)
* [micro-services-small-is-beautiful](http://www.slideshare.net/ewolff/micro-services-small-is-beautiful)
* [Martin Fowler: Microservices](http://martinfowler.com/articles/microservices.html)
* [what-are-micro-services](http://davidmorgantini.blogspot.com/2013/08/micro-services-what-are-micro-services.html)
* Book (Humble and Farley): [continuousdelivery.com](http://continuousdelivery.com/)
* [Netflix Blog: Deploying Netflix API](http://techblog.netflix.com/2013/08/deploying-netflix-api.html)
* [Mikey Cohen Netflix edge architecture, http://goo.gl/M159zi](http://goo.gl/M159zi)
* [Release It!](https://pragprog.com/book/mnee/release-it)


## Continuous Delivery

* Microservices lend themselves to continuous delivery.
* You actually *need* continuous delivery to extract maximum value.
* **New:** ALM support in Cloudfoundry from Cloudbees


## Cloudfoundry

* Environment Provisioning
* On-Demand/Automatic Scaling
* Failover/Resilience
* Routing/Front-end Load Balancing
* Monitoring

Deploying services needs to be simple and reproducible

```
$ cf push app.groovy
```

and you don't get much more convenient than that.

(Same argument for other PaaS solutions)


### Micro vs Monolithic... is NOT new

```
From:         kt4@prism.gatech.EDU (Ken Thompson)
Subject:      Re: LINUX is obsolete
Date:         3 Feb 92 23:07:54 GMT
Organization: Georgia Institute of Technology

I would generally agree that microkernels are probably the wave
of the future. However, it is in my opinion easier to implement
a monolithic kernel. It is also easier for it to turn into a
mess in a hurry as it is modified.

Regards, Ken
```

![mono-vs-micro-os](/images/mono-vs-micro-os.svg)


### What's wrong with a monolith?

![monolith](/images/monolith.jpg)