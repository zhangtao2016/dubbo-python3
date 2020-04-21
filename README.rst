.. role:: raw-html-m2r(raw)
   :format: html


Python Client For Apache Dubbo
------------------------------

Achieve load balancing on the client side、auto discovery service function with Zookeeper
-----------------------------------------------------------------------------------------

Python calls the Dubbo interface's jsonrpc protocol
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please use dubbo-rpc-jsonrpc and configure protocol in Dubbo for jsonrpc protocol\ :raw-html-m2r:`<br>`
*Reference* `https://github.com/apache/incubator-dubbo-rpc-jsonrpc <https://github.com/apache/incubator-dubbo-rpc-jsonrpc>`_

Installation
^^^^^^^^^^^^

Download code\ :raw-html-m2r:`<br>`
python setup.py install\ :raw-html-m2r:`<br>`
pip install\ :raw-html-m2r:`<br>`
pip install dubbo-python3>=1.0.1
Git install\ :raw-html-m2r:`<br>`
pip install git+\ `https://github.com/nickfan/dubbo-python3.git@1.0.1 <https://github.com/nickfan/dubbo-python3.git@1.0.1>`_

Load balancing on the client side, service discovery
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Get the registration information of the service through the zookeeper of the registry.\ :raw-html-m2r:`<br>`
Dubbo-client-py supports configuring multiple zookeeper service addresses. 
"host":"192.168.1.183:2181,192.168.1.184:2181,192.168.1.185:2181"\ :raw-html-m2r:`<br>`
Then the load balancing algorithm is implemented by proxy, and the server is called.\ :raw-html-m2r:`<br>`
Support Version and Group settings.

Example
^^^^^^^

.. code-block::

       config = ApplicationConfig('test_rpclib')
       service_interface = 'com.ofpay.demo.api.UserProvider'
       #Contains a connection to zookeeper, which needs caching.
       registry = ZookeeperRegistry('192.168.59.103:2181', config)
       user_provider = DubboClient(service_interface, registry, version='1.0')
       for i in range(1000):
       try:
           print(user_provider.getUser('A003'))
           print(user_provider.queryUser(
               {u'age': 18, u'time': 1428463514153, u'sex': u'MAN', u'id': u'A003', u'name': u'zhangsan'}))
           print(user_provider.queryAll())
           print(user_provider.isLimit('MAN', 'Joe'))
           print(user_provider('getUser', 'A005'))
       except DubboClientError as client_error:
           print(client_error)
       time.sleep(5)


TODO
^^^^

Optimize performance, minimize the impact of service upper and lower lines.\ :raw-html-m2r:`<br>`
Support Retry parameters\ :raw-html-m2r:`<br>`
Support weight call\ :raw-html-m2r:`<br>`
Unit test coverage   

Licenses
^^^^^^^^

Apache License

Thanks
^^^^^^

Thank @jingpeicomp for being a Guinea pig. It has been running normally for several months in the production environment. Thank you!
