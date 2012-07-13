Framework Benchmark
===================

Before, performance is not the most important thing when developing web applications, but, for example, Google decided_ to take site speed into account in the search rankings. This is yet another way in which improving web performance will have a positive impact.
Benchmarking below shows how efficient Phalcon is when compared with other traditional PHP frameworks. This benchmark is updated as stable versions are released from any of the frameworks mentioned or Phalcon itself. 

.. _decided: http://googlewebmastercentral.blogspot.com/2010/04/using-site-speed-in-web-search-ranking.html

Benchmarking below shows how efficient Phalcon is when compared with other traditional PHP frameworks. This benchmark is updated as stable versions are released from any of the frameworks mentioned or Phalcon itself. 

We allow you to clone the suite we're using for testing. You can download it to check which code was used to test the performance. If you have any additional optimizations or comments please `write us`_. `Check out source at Github`_

.. _write us: http://phalcon.uservoice.com/
.. _Check out source at Github: https://github.com/phalcon/framework-bench

.. versionadded:: 1.0	
	Update Mar-20-2012: Benchmarks has been remade changing the apc.stat setting to Off. More Info

.. versionchanged:: 1.1	
	Update May-13-2012: Benchmarks has been remade using PHP plain templating engine instead of Twig for Symfony. Configuration settings for Yii were also changed as recommended.

.. versionchanged:: 1.2
	Update May-20-2012: Fuel framework was added to benchmark.

.. versionchanged:: 1.3
	Update Jun-4-2012: Cake framework was added to benchmark. Actually, it isn't compared in the graphics because it takes 30 seconds to run only 10 of 1000. 


How the benchmark was made?
---------------------------

We made a "Hello World" benchmark looking to identify the minimal load overhead of each framework. Many people don't like this kind of benchmark because real-world applications need more complex features. However, these tests you will understand how much is the minimum time spent by each framework to perform a simple task. A task like this, is the minimal task that runs on every request made to an application.

In particular, this benchmark is only measuring the time it takes for a framework to start, run any action and freeing up resources to end the request. Any PHP application based on an MVC architecture will take as minimum those times. Also, note that this benchmark does not implement any complex feature, so in case of make a more large benchmark the time will be "hello world" (this) + complex features (db, templating, application logic, business rules, etc), so surely, these times will not decrease.

A controller and a view have been created for each framework. The controller "say" and action "hello". Action only gives a pass to the view for saying "Hello!". Using the "ab" benchmark tool we sent 1000 requests using 5 concurrent connections to each framework. 


What measures does were taken?
------------------------------

These were the measurements we take to measure the overall performance of the frameworks:

* Requests per second
* Time across all concurrent requests
* Number of included PHP files on a single request (measured using function get_included_files_.
* Memory Usage per request (measured using function memory_get_usage_.

.. _get_included_files: http://www.php.net/manual/en/function.get-included-files.php
.. _memory_get_usage: http://php.net/manual/en/function.memory-get-usage.php


What was the test environment?
------------------------------

APC_ intermediate code cache was enabled for all frameworks. Any Apache mod-rewrite feature was disabled to avoid possible extra overheads. 

.. _APC: http://php.net/manual/en/book.apc.php

The testing hardware environment is as follows: 

* Operating System: Mac OS X Snow Leopard 10.6.8
* Web Server: Apache httpd 2.2.21
* PHP: 5.3.8
* CPU: 3.06 Ghz Intel Core 2 Duo
* Main Memory: 4GB 1067 MHz DDR3
* Hard Drive: 500GB SCSI/SAS HDD 

*PHP version and info:*

.. image:: img/bench-1.png
	:align: center

*Apache environment:*

.. image:: img/bench-2.png
	:align: center

*APC settings:*

.. image:: img/bench-3.png
	:align: center

Results
-------	

Yii (YII_DEBUG=false) Version yii-1.1.10.r3566
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Yii_ is a high-performance PHP framework best for developing Web 2.0 applications. Version used for benchmark was yii-1.1.10.r3566. We disable YII_DEBUG for get faster perfomance. 

.. _Yii: http://www.yiiframework.com/

.. code-block:: php 

	# ab -n 1000 -c 5 http://localhost/bench/yii/index.php?r=say/hello
	This is ApacheBench, Version 2.3 <$Revision: 655654 $>
	Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
	Licensed to The Apache Software Foundation, http://www.apache.org/

	Benchmarking localhost (be patient)
	Completed 100 requests
	Completed 200 requests
	Completed 300 requests
	Completed 400 requests
	Completed 500 requests
	Completed 600 requests
	Completed 700 requests
	Completed 800 requests
	Completed 900 requests
	Completed 1000 requests
	Finished 1000 requests


	Server Software:        Apache/2.2.21
	Server Hostname:        localhost
	Server Port:            80

	Document Path:          /bench/yii/index.php?r=say/hello
	Document Length:        61 bytes

	Concurrency Level:      5
	Time taken for tests:   1.311 seconds
	Complete requests:      1000
	Failed requests:        0
	Write errors:           0
	Total transferred:      232000 bytes
	HTML transferred:       61000 bytes
	Requests per second:    762.55 [#/sec] (mean)
	Time per request:       6.557 [ms] (mean)
	Time per request:       1.311 [ms] (mean, across all concurrent requests)
	Transfer rate:          172.76 [Kbytes/sec] received

	Connection Times (ms)
	              min  mean[+/-sd] median   max
	Connect:        0    1   0.9      0       5
	Processing:     2    6   7.0      4      74
	Waiting:        0    5   5.7      4      60
	Total:          2    6   7.0      5      76
	WARNING: The median and mean for the initial connection time are not within a normal deviation
	        These results are probably not that reliable.

	Percentage of the requests served within a certain time (ms)
	  50%      5
	  66%      5
	  75%      7
	  80%      7
	  90%     10
	  95%     16
	  98%     29
	  99%     48
	 100%     76 (longest request)

Symfony Version 2.0.11
^^^^^^^^^^^^^^^^^^^^^^

Symfony_ is another high-performance PHP framework. 

.. _Symfony: http://symfony.com/

.. code-block:: php 

	# ab -n 1000 -c 5 http://localhost/bench/Symfony/web/app.php/say/hello/
	This is ApacheBench, Version 2.3 <$Revision: 655654 $>
	Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
	Licensed to The Apache Software Foundation, http://www.apache.org/

	Benchmarking localhost (be patient)
	Completed 100 requests
	Completed 200 requests
	Completed 300 requests
	Completed 400 requests
	Completed 500 requests
	Completed 600 requests
	Completed 700 requests
	Completed 800 requests
	Completed 900 requests
	Completed 1000 requests
	Finished 1000 requests


	Server Software:        Apache/2.2.21
	Server Hostname:        localhost
	Server Port:            80

	Document Path:          /bench/Symfony/web/app.php/say/hello/
	Document Length:        16 bytes

	Concurrency Level:      5
	Time taken for tests:   8.186 seconds
	Complete requests:      1000
	Failed requests:        0
	Write errors:           0
	Total transferred:      270000 bytes
	HTML transferred:       16000 bytes
	Requests per second:    122.15 [#/sec] (mean)
	Time per request:       40.932 [ms] (mean)
	Time per request:       8.186 [ms] (mean, across all concurrent requests)
	Transfer rate:          32.21 [Kbytes/sec] received

	Connection Times (ms)
	              min  mean[+/-sd] median   max
	Connect:        0    1   1.7      0      10
	Processing:    14   40  40.7     24     345
	Waiting:        0   39  40.2     24     345
	Total:         14   41  40.8     26     346

	Percentage of the requests served within a certain time (ms)
	  50%     26
	  66%     34
	  75%     43
	  80%     50
	  90%     92
	  95%    138
	  98%    162
	  99%    197
	 100%    346 (longest request)

CodeIgniter 2.1.0
^^^^^^^^^^^^^^^^^
CodeIgniter_ is a powerful PHP framework with a very small footprint, built for PHP coders who need a simple and elegant toolkit to create full-featured web applications.  

.. _CodeIgniter: http://codeigniter.com/

.. code-block:: php

	# ab -n 1000 -c 5 http://localhost/bench/codeigniter/index.php/say/hello
	This is ApacheBench, Version 2.3 <$Revision: 655654 $>
	Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
	Licensed to The Apache Software Foundation, http://www.apache.org/

	Benchmarking localhost (be patient)
	Completed 100 requests
	Completed 200 requests
	Completed 300 requests
	Completed 400 requests
	Completed 500 requests
	Completed 600 requests
	Completed 700 requests
	Completed 800 requests
	Completed 900 requests
	Completed 1000 requests
	Finished 1000 requests


	Server Software:        Apache/2.2.21
	Server Hostname:        localhost
	Server Port:            80

	Document Path:          /bench/codeigniter/index.php/say/hello
	Document Length:        16 bytes

	Concurrency Level:      5
	Time taken for tests:   1.184 seconds
	Complete requests:      1000
	Failed requests:        0
	Write errors:           0
	Total transferred:      187000 bytes
	HTML transferred:       16000 bytes
	Requests per second:    844.63 [#/sec] (mean)
	Time per request:       5.920 [ms] (mean)
	Time per request:       1.184 [ms] (mean, across all concurrent requests)
	Transfer rate:          154.24 [Kbytes/sec] received

	Connection Times (ms)
	              min  mean[+/-sd] median   max
	Connect:        0    1   0.7      0       5
	Processing:     2    5  11.0      4     148
	Waiting:        0    5  10.8      4     148
	Total:          2    6  10.9      4     148	

	Percentage of the requests served within a certain time (ms)
	  50%      4
	  66%      4
	  75%      5
	  80%      6
	  90%      8
	  95%     12
	  98%     24
	  99%     38
	 100%    148 (longest request)

Kohana 3.2.0
^^^^^^^^^^^^
Kohana_ is an elegant HMVC PHP5 framework that provides a rich set of components for building web applications.

.. _Kohana: http://kohanaframework.org/index

.. code-block:: php 

	# ab -n 1000 -c 5 http://localhost/bench/kohana/index.php/say/hello
	This is ApacheBench, Version 2.3 <$Revision: 655654 $>
	Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
	Licensed to The Apache Software Foundation, http://www.apache.org/

	Benchmarking localhost (be patient)
	Completed 100 requests
	Completed 200 requests
	Completed 300 requests
	Completed 400 requests
	Completed 500 requests
	Completed 600 requests
	Completed 700 requests
	Completed 800 requests
	Completed 900 requests
	Completed 1000 requests
	Finished 1000 requests


	Server Software:        Apache/2.2.21
	Server Hostname:        localhost
	Server Port:            80

	Document Path:          /bench/kohana/index.php/say/hello
	Document Length:        15 bytes

	Concurrency Level:      5
	Time taken for tests:   1.603 seconds
	Complete requests:      1000
	Failed requests:        0
	Write errors:           0
	Total transferred:      186000 bytes
	HTML transferred:       15000 bytes
	Requests per second:    623.77 [#/sec] (mean)
	Time per request:       8.016 [ms] (mean)
	Time per request:       1.603 [ms] (mean, across all concurrent requests)
	Transfer rate:          113.30 [Kbytes/sec] received

	Connection Times (ms)
	              min  mean[+/-sd] median   max
	Connect:        0    1   0.9      0       5
	Processing:     2    7  22.4      5     317
	Waiting:        0    7  22.3      4     317
	Total:          2    8  22.3      5     318	

	Percentage of the requests served within a certain time (ms)
	  50%      5
	  66%      5
	  75%      6
	  80%      7
	  90%     10
	  95%     17
	  98%     33
	  99%     46
	 100%    318 (longest request)


Fuel 1.2
^^^^^^^^
FuelPHP_ is a simple, flexible, community driven PHP 5.3 web framework based on the best ideas of other frameworks with a fresh start. 

.. _FuelPHP: http://fuelphp.com/

.. code-block:: php 

	# ab -n 1000 -c 5 http://localhost/bench/fuel/say/hello
	This is ApacheBench, Version 2.3 <$Revision: 655654 $>
	Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
	Licensed to The Apache Software Foundation, http://www.apache.org/

	Benchmarking localhost (be patient)
	Completed 100 requests
	Completed 200 requests
	Completed 300 requests
	Completed 400 requests
	Completed 500 requests
	Completed 600 requests
	Completed 700 requests
	Completed 800 requests
	Completed 900 requests
	Completed 1000 requests
	Finished 1000 requests


	Server Software:        Apache/2.2.21
	Server Hostname:        localhost
	Server Port:            80

	Document Path:          /bench/fuel/say/hello
	Document Length:        16 bytes

	Concurrency Level:      5
	Time taken for tests:   1.771 seconds
	Complete requests:      1000
	Failed requests:        0
	Write errors:           0
	Total transferred:      187000 bytes
	HTML transferred:       16000 bytes
	Requests per second:    564.49 [#/sec] (mean)
	Time per request:       8.857 [ms] (mean)
	Time per request:       1.771 [ms] (mean, across all concurrent requests)
	Transfer rate:          103.09 [Kbytes/sec] received

	Connection Times (ms)
	              min  mean[+/-sd] median   max
	Connect:        0    1   1.0      0       6
	Processing:     3    8   9.2      6      80
	Waiting:        0    7   7.2      5      80
	Total:          3    9   9.2      6      81

	Percentage of the requests served within a certain time (ms)
	  50%      6
	  66%      7
	  75%      9
	  80%     10
	  90%     16
	  95%     23
	  98%     43
	  99%     59
	 100%     81 (longest request)

Cake 2.1.3
^^^^^^^^^^
CakePHP_ makes building web applications simpler, faster and require less code. **Unlike others, we are measuring only 10 requests of 1000, if you know how to improve this results please write us.**

.. _CakePHP: http://cakephp.org/

.. code-block:: php 

	# ab -n 10 -c 5 http://localhost/bench/cake/say/hello
	This is ApacheBench, Version 2.3 <$Revision: 655654 $>
	Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
	Licensed to The Apache Software Foundation, http://www.apache.org/

	Benchmarking localhost (be patient).....done


	Server Software:        Apache/2.2.22
	Server Hostname:        localhost
	Server Port:            80

	Document Path:          /bench/cake/say/hello
	Document Length:        16 bytes

	Concurrency Level:      5
	Time taken for tests:   30.051 seconds
	Complete requests:      10
	Failed requests:        0
	Write errors:           0
	Total transferred:      1680 bytes
	HTML transferred:       160 bytes
	Requests per second:    0.33 [#/sec] (mean)
	Time per request:       15025.635 [ms] (mean)
	Time per request:       3005.127 [ms] (mean, across all concurrent requests)
	Transfer rate:          0.05 [Kbytes/sec] received

	Connection Times (ms)
	              min  mean[+/-sd] median   max
	Connect:        0    2   3.6      0      11
	Processing: 15009 15020   9.8  15019   15040
	Waiting:        9   21   7.9     25      33
	Total:      15009 15022   8.9  15021   15040

	Percentage of the requests served within a certain time (ms)
	  50%  15021
	  66%  15024
	  75%  15024
	  80%  15032
	  90%  15040
	  95%  15040
	  98%  15040
	  99%  15040
	 100%  15040 (longest request)

Phalcon Version 0.3.5
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: php

	# ab -n 1000 -c 5 http://localhost/bench/phalcon/?_url=say/hello
	This is ApacheBench, Version 2.3 <$Revision: 655654 $>
	Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
	Licensed to The Apache Software Foundation, http://www.apache.org/

	Benchmarking localhost (be patient)
	Completed 100 requests
	Completed 200 requests
	Completed 300 requests
	Completed 400 requests
	Completed 500 requests
	Completed 600 requests
	Completed 700 requests
	Completed 800 requests
	Completed 900 requests
	Completed 1000 requests
	Finished 1000 requests


	Server Software:        Apache/2.2.21
	Server Hostname:        localhost
	Server Port:            80

	Document Path:          /bench/phalcon/?_url=say/hello
	Document Length:        16 bytes

	Concurrency Level:      5
	Time taken for tests:   0.385 seconds
	Complete requests:      1000
	Failed requests:        0
	Write errors:           0
	Total transferred:      187000 bytes
	HTML transferred:       16000 bytes
	Requests per second:    2599.46 [#/sec] (mean)
	Time per request:       1.923 [ms] (mean)
	Time per request:       0.385 [ms] (mean, across all concurrent requests)
	Transfer rate:          474.71 [Kbytes/sec] received

	Connection Times (ms)
	              min  mean[+/-sd] median   max
	Connect:        0    0   0.3      0       3
	Processing:     1    2   1.9      1      43
	Waiting:        0    1   1.8      1      43
	Total:          1    2   1.9      2      43

	Percentage of the requests served within a certain time (ms)
	  50%      2
	  66%      2
	  75%      2
	  80%      2
	  90%      3
	  95%      4
	  98%      5
	  99%      9
	 100%     43 (longest request)

Graphs
^^^^^^

The first graph shows how many requests per second each framework was able to accept. Second shows the average time across all concurrent requests. 

???? NO SE COLOCAR IMAGENES DE BARRAS

Conclusion
-----------

The Phalcon compiled nature offers extraordinary performance that outperforms all other frameworks in this comparison. Phalcon is a real high performance framework that allows you to scale more easily than ever. 