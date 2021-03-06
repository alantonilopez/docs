Class **Phalcon_Model_MetaData_Session**
========================================

Stores model meta-data in session. Data will erase when the session finishes.  Meta-data are permanent while the session is active.   You can query the meta-data by printing $_SESSION['$PMM$']  

.. code-block:: php

    <?php

    
     $modelManager = new Phalcon\Model\Manager();
    
     $metaData = new Phalcon\Model\Metadata('Session', array(
        'suffix' => 'my-app-id'
     ));
     $modelManager->setMetaData($metaData);

Methods
---------

**__construct** (Phalcon_Config|stdClass $options)

Phalcon_Model_MetaData_Session constructor

**array** **read** ()

Reads meta-data from $_SESSION

**write** (array $data)

Writes the meta-data to $_SESSION

