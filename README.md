# starter package:

### Start: All the coding program is finish by Python, the application I used to finish coding is [PyCharm](https://www.jetbrains.com/pycharm/download/?section=windows#section=windows)  
    ```
    
    ```
### ChatGPTs for Research  
()[]  
### 1. Python GUI(graphical user interface):  
   Most of the users have no idea about coding part, so GUI is a good one for user experience.  
   GUI can form an interface that users will directly see diagrams or the data without coding experience.  

### 2. Resources to visualize the data  
   #### 2.1 matplotlib  
   --It can be usded to visualize pairwise data/ statistical distribution/ irregular data/ 3D plot  
   --Right now, we only consider the 2d (x,y) plot and 3d (x,y,z) plot  
   --exp 2d plot:  
   ![](https://matplotlib.org/stable/_images/sphx_glr_plot_001.png)  
   ```
   pip install xxxx
   # This is the format in terminal to install the library you need
   ```
   ```
   import matplotlib.pyplot as plt
   import numpy as np

   plt.style.use('_mpl-gallery')

   # make data
   x = np.linspace(0, 10, 100)
   y = 4 + 2 * np.sin(2 * x)

   # plot
   fig, ax = plt.subplots()

   ax.plot(x, y, linewidth=2.0)

   ax.set(xlim=(0, 8), xticks=np.arange(1, 8),
          ylim=(0, 8), yticks=np.arange(1, 8))

   plt.show()
   ```
   
   #### 2.2 PyQt5  
   --The first part I have talked about we might need GUI for users, the user interface can be done by PyQt5(structure) and matplotlib(visualization).  
   --PyQt5 is an application for design the GUI interface, it can connect ui interface and python codes.(This is finished by converting the .ui output to .py files)  
   --PyQt5 intro:  
       step1: download [PyQt5](https://www.qt.io/download)  
       step2: open Qt Creator on your computer, create new project -> Qt for Python -> Window UI ![](https://codehs.com/uploads/fd63edb6633b2b822e9d85bcd4f24d5b)  
       step3: double click the .ui file. ![](https://codehs.com/uploads/0e1e721f30d1a382da8fc3d5d180a2a0)  
       step4: drag what you need for this gui. ![](https://codehs.com/uploads/140ff30f0902590d41fa885084824ddc)  
   
   #### 2.3 pyvisa  
   --each code driven instrument has their specific lib  
   --for the Keithley 2400, the lib for this instrument is pyvisa  
   [pyvisa lib](https://pyvisa.readthedocs.io/en/latest/)  

   --The instrument driver for Keithley 2400 are [488.2](https://www.ni.com/en/support/downloads/drivers/download.ni-488-2.html#484357) and [NI Visa](https://www.ni.com/en/support/downloads/drivers/download.ni-visa.html#521671) and [NI Max](https://www.ni.com/en/support/downloads/drivers/download.system-configuration.html#521523)
   
   --Open NI Max, and then connect the intrument address  
   --use the following codes to test if the connection is successful  
   
   ```
   import pyvisa

   rm = pyvisa.ResourceManager()
   resources = rm.list_resources()
   print("Available Resources:")
   for resource in resources:
       print(resource)
   ```

   
   
### 3. Instruments  
