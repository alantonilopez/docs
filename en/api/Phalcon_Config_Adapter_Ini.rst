Class **Phalcon_Config_Adapter_Ini**
====================================

Reads ini files and convert it to Phalcon_Config objects.   Given the next configuration file:   

.. code-block:: php

    <?php

    
     $config = new Phalcon_Config_Adapter_Ini("path/config.ini")
    
     echo $config->phalcon->controllersDir;
     echo $config->database->username;
     



   You can read it as follows:   

.. code-block:: php

    <?php

    
     $config = new Phalcon_Config_Adapter_Ini("path/config.ini")
    
     echo $config->phalcon->controllersDir;
     echo $config->database->username;

Methods
---------

**Phalcon_Config_Adapter_Ini** **__construct** (string $filePath)

Phalcon_Config_Adapter_Ini constructor

