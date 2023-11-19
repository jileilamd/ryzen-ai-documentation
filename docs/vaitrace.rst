Run Vitis AI Profiler
=====================

vai_trace
---------

.. Note::
    
    Before start profiler example, you should run voe onnx Example successfully

**vaitrace shows an ASCII table**

For C++ programs, add vaitrace in front of the test command, the test command is:
  .. code-block:: bash
    
    # python %cd%\..\bin\vaitrace\vaitrace.py -t [timeout] --txt  your-test-command.
  
vaitrace prints an ASCII table as shown in the following figure

.. image:: ../images/profiler-txt.png
   :width: 1600px
   :alt: vaitrace --txt block diagram

If you set XLNX_ENABLE_DEBUG_MODE=1 vaitrace could get the info of every super layer

The command is:

  .. code-block:: bash

    # python %cd%\..\bin\vaitrace\vaitrace.py -t [timeout] --txt --fine_grained  your-test-command.

* **DPU SubGraph**: Name of subgraph in the xmodel
* **WL**: Computation workload (MAC indicates two operations, only available for conv subgraphs now)
* **SW_RT**: The execution time calculate by software in Microseconds
* **HW_RT**: The execution time from hardware counter in Microseconds
* **Effic**: The DPU actual performance divided by peak theoretical performance
* **LdWB**: External memory load size of bias and weight
* **LdFM**: External memory load size of feature map
* **StFM**: External memory store size of feature map
* **TOTAL_SW_RT**: sum of all super layers SW_RT
* **SUPER_LAYER_COUT**: all super layers of xmodel

**vaitrace shows in csv format**

If you want to show result by csv or excel, you should run above command with "--csv" and you could get 
vaitrace-platforname-modelname.csv file in current path.

* If using the command line, run 
  
  .. code-block:: bash

   # python %cd%\..\bin\vaitrace\vaitrace.py -t [timeout] --csv --fine_grained  your-test-command.

vaitrace output an csv file name: vaitrace-paltfom-modelname.csv 

**vaitrace Usage**

**Command Line Usage**
  
.. code-block:: bash
  
 usage: vaitrace [-h] [-c [CONFIG]] [-d] [-o [TRACESAVETO]] [-t [TIMEOUT]] [-v] 
                 [-b] [-p] [--va] [--xat] [--txt_summary] [--json_summary] [--csv_summary] [--fine_grained] ...
    
 positional arguments:
    
 cmd

 options:
 -h, --help        show this help message and exit
 -c [CONFIG]       Specify the config file
 -d                Enable debug
 -o [TRACESAVETO]  Save report to, only available for txt summary mode
 -t [TIMEOUT]      Tracing time limit in second, default value is 60
 -v                Show version
 -b                Bypass vaitrace, just run command
 -p                Trace python application
 --va              Generate trace data for Vitis Analyzer
 --xat             Save raw data, for debug usage
 --txt_summary     Display txt summary
 --json_summary    Display json summary
 --csv_summary     Display csv summary
 --fine_grained    Fine grained mode

**Important and frequently used arguments**

 * **cmd**: cmd is your executable program of Vitis AI that to be traced, including program name and arguments
 * **t**: control the tracing time(in seconds) starting from the [cmd] being launched.
 * **c**: we can start a tracing with more custom options by writing these options on a json configuration 
   file and specify the configuration by -c, details of configuration file will be explained in the next section
 * **o**: where to save report, only available for text summary mode, by default, the test summary will be output to STDOUT
 * **txt**: Output text summary
 * **csv**: Output csv summary
 * **fine_grained**: Contronling the trace hierarchical information or not



Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file
except in compliance with the License.

You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0


Unless required by applicable law or agreed to in writing, software distributed under the
License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
either express or implied. See the License for the specific language governing permissions
and limitations under the License.
