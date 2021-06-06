---
layout: post
title: [Multiprocessing] Pool vs Process
date : 30 Jun 2021
category : ML_Preprocess
comments : true
---
 : 일부 반복적인 작업 과정에서 1개의 Process만을 사용함에 따라, 작업시간이 오래걸리는 문제를 해결하기 위해 MultiProcessing에 대해서 공부해보고자한다.

# 1. Multi-Processing vs Multi-Thread

### (1) Thread?? Processing??
: MultiProcessing에 앞서서, 우선 Thread와 Processor에 대한 정의와 차이부터 살펴보자. 컴공 지식에 대해서는 잘 모르기에, 내가 알 수 있는 깊이에서 둘 간의 차이점을 살펴보자.

|  | Thread | Processe |
|---|---|---|
|정의| 프로세스내에서 실제로 작업을 수행하는 주체 | 실행 중인 프로그램 |
|   | 모든 프로세스에는 한개 이상의 스레드(thread)가 존재하여 작업을 진행함. | 사용자가 작성한 프로그램이 운영체제에 의해 메모리 공간을 할당받아 실행 중인 것. |
|   | 하나의 프로세스에 2개 이상의 스레드(thread)를 갖는 것을 multi-Thread process라고함. | 프로세스는 프로그램에 사용되는 '데이터', '메모리 등의 자원', '스레드'로 구성됨.|
|메모리 공유| 메모리를 공유하여, 각 cpu가 서로의 상태를 공유할 수 있음. |  메모리를 공유하지 않음 |
|Interrupt &kill| Interrupt & kill 불가능 |  메모리를 공유하여, 각 cpu가 서로의 상태를 공유할 수 있음. |
|Thread의 장점| 1) 프로세스보다 생성 및 종료시간, 쓰레드간 전환시간이 짧다. |  |
|           | 2) 프로세스의 메모리, 자원등을 공유하기에, 커널의 도움 없이 상호통신이 가능하다. |  |

여기까지 살펴보았을 때, 우리의 목표는 하나의 파이썬이라는 프로세스(프로그램)에서 여러개의 쓰레드를 띄워 필요한 작업을 병렬로 처리하면 될 것으로 보인다.

### (2) GIL(Global Interpreter Lock)
 : 그러나 슬프게도(?) 파이썬에서는 여러개의 쓰레드를 사용하는 Multi-Thread를 지원하지 않는다.
  파이썬은  global변수로 하나의 인터프리터가 실행된다. 만약 쓰레드가 동시에 작동한다면, global변수를 함께 공유하게 될 것이고, 특정 스레드가 global변수를 변경할시, 동일한 변수에 접근해있던 다른 쓰레드는 엉망이 되어버릴 것이기에 *한번에 하나의 Thread만이 인터프리너 내부의 global변수에 접근할 수 있도록 해놓았다.(GIL)*(하나의 thread만이 접근가능한 일부 틀릴 수 있음.)

  따라서 파이썬에서는 Multi Thread를 사용하더라도, Lock으로 인하여 한번에 하나의 Thread만 실행되기에, 되려 Multi core CPU라고 하더라도 실행시간이 효과가 없거나 되려 늘어나버릴 수 있다.

# 2. Multi-Processing


#### Refernce
##### 1. Multi-Processing vs Multi-Thread
[1] [Thread란?](http://tcpschool.com/java/java_thread_concept)  
[2] [Thread와 MultiProcessing 차이점](https://www.ellicium.com/python-multiprocessing-pool-process)  
##### 2. Multi-Processing
[2] [Python Multiprocessing: Pool vs Process – Comparative Analysis](https://www.ellicium.com/python-multiprocessing-pool-process)  
