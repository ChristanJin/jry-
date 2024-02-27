# starter package:

### Start: All the coding program is finish by Python, the application I used to finish coding is [PyCharm](https://www.jetbrains.com/pycharm/download/?section=windows#section=windows)  
    ```
    using it
    ```

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
   PyQt5 is an application that we can use formal user interface's properties to design an interface without coding.  
   
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
   3.1 K2400  
    --K2400 is an instrument using PyVisa lib, we can remotely use codes to connect the hardware instruments and achive our goals.  
    --Here are the exp codes to drive k2400
    
```
    # import necessary libs
    import sys
    sys.path.append('./Qcodes')
    from qcodes.instrument_drivers.tektronix.Keithley_2400 import Keithley_2400 as Keithley2400
    
    import pyvisa
    
    # open Keithley 2400
    rm = pyvisa.ResourceManager()
    try:
        instrument = rm.open_resource('ASRL4::INSTR')  # replace with correct infor
        identity = instrument.query('*IDN?')
        print('Instrument Identity:', identity)
    except Exception as e:
        print('Error:', e)
    finally:
        instrument.close()
    
    
    use_random = 0 #for test only!!! Set to 0 in real experiments!!!!
    
    # define a control function for Keithley 2400
    def control_k2400():
        try:
            # initialized Keithley 2400
            k2400 = Keithley2400(name='k2400', address='10')
    
            # set up Keithley 2400
            k2400.source_voltage(0.1)  # 设置电压源电压为0.1 V
    
            # action
            current = k2400.measure_current()
    
            # print
            print(f"Measured Current: {current} A")
    
        except Exception as e:
            # catch possible errors
            print(f"An error occurred: {str(e)}")
    
        finally:
            # close it
            k2400.disconnect()
            print("Keithley 2400 disconnected.")
    
    # 主程序入口
    if __name__ == '__main__':
        # use the function to control K2400
        control_k2400()
```
   --Here are the exp codes on how to drive intrument. Later I will explain step by step:
   --a. connection between hardware and local address:
```
    123
```
