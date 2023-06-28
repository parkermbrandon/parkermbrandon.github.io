## Library startup, shutdown, and error handling

```C++
void configureAIO()
{
    // Initialize the shared library
    AIO_initialize();

    // Check if an AIO is connected
    std::cout << "AIO connected: " << AIO_isAIOConnected() << std::endl;

    // Always call AIO_shutdown before unloading the library
    AIO_shutdown();
}
```

```Python
import ctypes

import EchoAIOInterface

#
#    Change the following path to the location of EchoAIOInterface.dll.
#    The default location is C:\Progam Files\Echo AIO\CLI + API\EchoAIOInterface.dll
#
path = 'C:\Program Files\Echo AIO\CLI + API\EchoAIOInterface.dll'
echoaio = ctypes.WinDLL(path)

#
#    Call AIO_initialize() before  calling any other function to set up the library.
#
echoaio.AIO_initialize()

#
#    Call AIO_shutdown() before unloading the library to release memory and resources
#
echoaio.AIO_shutdown.restype = None
echoaio.AIO_shutdown()
```
# Library startup and shutdown
### AIO_initialize

```C++
void AIO_initialize();
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Call AIO_initialize before calling any other library functions to set up the library



### AIO_shutdown

```C++
void AIO_shutdown();
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Call AIO_shutdown before unloading the library to release memory and resources



### AIO_getErrorString

```C++
void AIO_getErrorString(char *const text, size_t textBufferBytes);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns a string describing the last error

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**text** char *const: text Pointer to the buffer to receive the zero-terminated UTF-8 encoded string

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**textBufferBytes** size_t: textBufferBytes Length of the buffer in bytes



# AIO inquiry
### AIO_getLibraryVersion

```C++
void AIO_getLibraryVersion(char *const text, size_t textBufferBytes);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Gets the library version as a zero-terminated UTF-8 encoded string

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**text** char *const: text Pointer to the buffer to receive the zero-terminated UTF-8 encoded string

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**textBufferBytes** size_t: textBufferBytes Length of the buffer in bytes




### AIO_isAIOConnected

```C++
int AIO_isAIOConnected();
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Check if an AIO is connected to this computer
#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Non-zero value if an AIO is connected



### AIO_getNumInputChannels

```C++
int AIO_getNumInputChannels();
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get the number of analog and digital audio input channels for the connected AIO
#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The total number of input channels for the AIO



### AIO_getNumOutputChannels

```C++
int AIO_getNumOutputChannels();
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get the number of analog and digital audio output channels for the connected AIO
#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The total number of output channels for the AIO



### AIO_hasComboModule

```C++
int AIO_hasComboModule(int moduleSlot);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Check if this AIO has an AIO-C module in a slot

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**moduleSlot** int: moduleSlot 0 for center audio module slot, 1 for outer audio module slot

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Non-zero value if an AIO is connected and if the AIO has an AIO-C module in the specified slot



### AIO_hasTModule

```C++
int AIO_hasTModule(int moduleSlot);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Check if this AIO has an AIO-T module in a slot

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**moduleSlot** int: moduleSlot 0 for center audio module slot, 1 for outer audio module slot

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Non-zero value if an AIO is connected and if the AIO has an AIO-T module in the specified slot



### AIO_hasBluetoothModule

```C++
int AIO_hasBluetoothModule(int moduleSlot);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Check if this AIO has an AIO-B module in a slot

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**moduleSlot** int: moduleSlot 0 for center audio module slot, 1 for outer audio module slot

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Non-zero value if an AIO is connected and if the AIO has an AIO-B module in the specified slot



### AIO_getModuleType

```C++
int AIO_getModuleType(int moduleSlot);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get the module type for the specified slot

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**moduleSlot** int: moduleSlot 0 for center audio module slot, 1 for outer audio module slot

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The module type for the specified slot


### 
```C++
AIO_moduleTypeUnknown: -1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Unknown module type
```C++
AIO_moduleTypeNone: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Module not detected
```C++
AIO_moduleTypeA: 1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO-A module
```C++
AIO_moduleTypeS: 2
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO-S module
```C++
AIO_moduleTypeL: 3
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO-L module
```C++
AIO_moduleTypeC: 4
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO-C module
```C++
AIO_moduleTypeH: 5
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO-H module
```C++
AIO_moduleTypeT: 6
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO-T module
```C++
AIO_moduleTypeB: 7
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO-B module
# AIO module parameter functions
### AIO_getModuleIntParameter

```C++
int AIO_getModuleIntParameter(int moduleSlot, int parameter, int *const value);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retrieves an integer parameter for a module

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**moduleSlot** int: moduleSlot 0 for center audio module slot, 1 for outer audio module slot

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**parameter** int: parameter Parameter number (e.g. AIO_comboParameterAuxOut)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**value** int *const: value Pointer to the integer variable to receive the parameter value

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful



### AIO_setModuleIntParameter

```C++
int AIO_setModuleIntParameter(int moduleSlot, int parameter, int value);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sets an integer parameter for a module

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**moduleSlot** int: moduleSlot 0 for center audio module slot, 1 for outer audio module slot

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**parameter** int: parameter Parameter number (e.g. AIO_comboParameterAuxOut)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**value** int: value Integer parameter value

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful



### AIO_getModuleDoubleParameter

```C++
int AIO_getModuleDoubleParameter(int moduleSlot, int parameter, double *const value);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retrieves a double-precision floating-point parameter for a module

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**moduleSlot** int: moduleSlot 0 for center audio module slot, 1 for outer audio module slot

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**parameter** int: parameter Parameter number (e.g. AIO_comboParameterOverCurrentThresholdAmperes)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**value** double *const: value Pointer to the double-precision floating-point variable to receive the parameter value

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful



### AIO_setModuleDoubleParameter

```C++
int AIO_setModuleDoubleParameter(int moduleSlot, int parameter, double value);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sets a double-precision floating-point parameter for a module

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**moduleSlot** int: moduleSlot 0 for center audio module slot, 1 for outer audio module slot

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**parameter** int: parameter Parameter number (e.g. AIO_comboParameterAuxOut)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**value** double: value Double-precision floating-point parameter value

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful


# Windows audio functions
### AIO_getASIOPreferredBufferSize

```C++
int AIO_getASIOPreferredBufferSize();
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retrieves the preferred buffer size for the ASIO audio driver
#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The ASIO driver preferred buffer size in samples



### AIO_setASIOPreferredBufferSize

```C++
int AIO_setASIOPreferredBufferSize(int bufferSize);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sets the preferred buffer size for the ASIO audio driver

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**bufferSize** int: bufferSize Preferred buffer size in samples

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful



### AIO_getSampleRate

```C++
int AIO_getSampleRate();
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retrieves the current buffer size for the ASIO audio driver
#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current sample rate in Hz



### AIO_setSampleRate

```C++
int AIO_setSampleRate(int sampleRate);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sets the sample rate for the ASIO audio driver

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**sampleRate** int: sampleRate Sample rate in Hz

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful


Common settings for AIO-A, AIO-L, AIO-S, and AIO-H modules
Get and set mic/line input gain and constant current power; read TEDS data
# AIO mic inputs
### AIO_hasInputGainControl

```C++
int AIO_hasInputGainControl(int inputChannel);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Checks whether the specified input channel has a gain control feature

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**inputChannel** int: inputChannel    Input channel number, starting at 0

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;true if inputChannel has an input gain control



### AIO_getInputGain

```C++
int AIO_getInputGain(int inputChannel, int* const gain);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retrieves the gain value for the specified input channel, and stores the result in the memory location pointed to by 'gain'.

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**inputChannel** int: inputChannel    Input channel number, starting at 0

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**gain** int* const: gain            Pointer to the variable to receive the gain value

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful



### AIO_setInputGain

```C++
int AIO_setInputGain(int inputChannel, int gain);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sets the gain value for the specified input channel

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**inputChannel** int: inputChannel    Input channel number, starting at 0

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**gain** int: gain            Gain value (1, 10, or 100)

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful



### AIO_hasConstantCurrentControl

```C++
int AIO_hasConstantCurrentControl(int inputChannel);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Checks whether the specified input channel has a constant current power supply

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**inputChannel** int: inputChannel    Input channel number, starting at 0

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;true if inputChannel has a constant current power supply



### AIO_getConstantCurrentState

```C++
int AIO_getConstantCurrentState(int inputChannel, int* const enabled);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retrieves the constant current power setting for the specified input channel, and stores the result in the memory location pointed to by 'enabled'.

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**inputChannel** int: inputChannel    Input channel number, starting at 0

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**enabled** int* const: enabled         Pointer to the variable to receive the constant current power setting

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful



### AIO_setConstantCurrentState

```C++
int AIO_setConstantCurrentState(int inputChannel, int enabled);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sets the constant current power setting for the specified input channel

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**inputChannel** int: inputChannel    Input channel number, starting at 0

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**enabled** int: enabled         0 to disable the constant current power, 1 to enable

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful



### AIO_hasTEDS

```C++
int AIO_hasTEDS(int inputChannel);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Checks whether the specified input channel has TEDS data

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**inputChannel** int: inputChannel    Input channel number, starting at 0

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;true if inputChannel can read TEDS data



### AIO_getTEDSProperties

```C++
int AIO_getTEDSProperties(int inputChannel, char* const jsonText, size_t jsonBufferBytes, size_t* jsonBytesRequired);
```

>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retrieves the TEDS data for the specified input channel and writes the TEDS data to the specified buffer as JSON-formatted text. 'jsonText' and 'jsonBytesRequired' are optional parameters.

#### Parameters:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**inputChannel** int: inputChannel        Input channel number, starting at 0

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**jsonText** char* const: jsonText            Points to a buffer to receive the JSON-formatted text

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**jsonBufferBytes** size_t: jsonBufferBytes     Length of the JSON text buffer in bytes

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**jsonBytesRequired** size_t*: jsonBytesRequired   Points to a value to receive the number of bytes needed for the JSON text buffer

#### Returns:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO_OK if successful


Get and set mic/line input gain and constant current power; read TEDS data
Common settings for AIO-A, AIO-L, AIO-S, and AIO-H modules
AIO-C configuration constants and parameters
### Integer parameters for configuring an AIO-C module (see AIO_setModuleIntParameter and AIO_getModuleIntParameter)

```C++
AIO_comboParameterFirmwareVersion: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Module firmware version
```C++
AIO_comboParameterSerialNumber: 1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Module serial number
```C++
AIO_comboParameterAuxOut: 2
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AUX OUT pin settings\n \n Bits 0-7 of the value are a bit mask corresponding to the state of the AUX OUT pins
```C++
AIO_comboParameterAuxIn: 3
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Read-only value for AUX IN\n \n  bits 0-7 of the value are a bit mask corresponding to the state of the AUX IN pins
```C++
AIO_comboParameter5VDCEnable: 4
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Enable or disable the 5 VDC power supply\n \n 0 to disable, 1 to enable
```C++
AIO_comboParameterVariableDCPowerEnable: 5
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Enable or disable the variable DC power supply\n \n 0 to disable, 1 to enable
```C++
AIO_comboParameterVariableDCPowerOutputMillivolts: 6
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sets the battery simulator output voltage in millivolts, from 600 mV to 5000 mV
```C++
AIO_comboParameterVariableDCPowerMeasuredMillivolts: 7
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reads the actual measured voltage in millivolts for the variable DC power supply
```C++
AIO_comboParameterMeasuredCurrentRange: 8
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the battery simulator current measurement range; must be one of the AIO_comboCurrentMeasurementRange values
```C++
AIO_comboParameterOverCurrentCondition: 9
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If this parameter value reads as true, then then AIO-C module has detected an over current condition. Set this parameter to zero to clear the over current condition
### Floating-point parameters for configuring an AIO-C module (see AIO_setModuleDoubleParameter and AIO_getModuleDoubleParameter)

```C++
AIO_comboParameterVariableDCPowerMeasuredAmperes: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reads the measured output current in amperes for the battery simulator
```C++
AIO_comboParameterOverCurrentThresholdAmperes: 1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set or get the overcurrent threshold in amperes; note that the allowable value range for this parameter is determined by the measured current range
### DC current measurement ranges for the AIO-C module battery simulator

```C++
AIO_comboCurrentMeasurementRange_250uA: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 to 256 microamps
```C++
AIO_comboCurrentMeasurementRange_1250uA: 1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 to 1280 microamps
```C++
AIO_comboCurrentMeasurementRange_250mA: 2
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 to 256 milliamps
```C++
AIO_comboCurrentMeasurementRange_1250mA: 3
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 to 1280 milliamps
AIO-C configuration constants and parameters
AIO-H configuration constants and parameters
### Configure the impedance measurement channel for an AIO-H module (see AIO_setModuleIntParameter and AIO_getModuleIntParameter)

```C++
AIO_headphoneParameterImpedanceSelect: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;selects impedance measurement for the left headphone output or the right
### Parameter values for AIO_headphoneParameterImpedanceSelect

```C++
AIO_headphoneImpedanceLeft: 1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Select left headphone channel for impedance measurement
```C++
AIO_headphoneImpedanceRight: 2
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Select right headphone channel for impedance measurement
AIO-H configuration constants and parameters
AIO-T configuration constants and parameters
### Parameters for configuring an AIO-T module (see AIO_setModuleIntParameter and AIO_getModuleIntParameter)

```C++
AIO_tdmParameterFirmwareVersion: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Module firmware version
```C++
AIO_tdmParameterBitsPerWord: 1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Number of bits per TDM word: 24 or 32 bits
```C++
AIO_tdmParameterBitsPerFrame: 2
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Number of bits per TDM frame: 64, 128, or 256 bits/frame
```C++
AIO_tdmParameterFSYNCPhaseDelay: 3
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FSYNC phase delay cleared: FSYNC clocks out aligned with audio data
                           0 - INPUT is sampled normally, 
FSYNC phase delay set:     FSYNC is delayed by 1/2 SCLK cycle
 1 - INPUT sampling is delayed by 1 / 2 SCLK cycle
```C++
AIO_tdmParameterInvertSCLK: 4
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SCLK polarity: 0 - data and FSYNC clocks out on the falling edge of SCLK, 1 - Data and FSYNC clocks out on the rising edge of SCLK
```C++
AIO_tdmParameterAudioDataShiftEnabled: 5
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Clock source mode] Integer parameter that delays the sampling of input SHIFT bits; 0 - TDM input sampling is aligned with TDM input, 1 - TDM output is advanced N bits adead of the TDM input.
[Clock sink mode] Integer parameter that enables SCLK output on BNC connector(Only valid for versions prior to 2.01. Must be set for versions 2.01 thru 2.0e, ignored for 2.0f and above)
```C++
AIO_tdmParameterClockMode: 6
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the module to clock source or clock sink mode (see AIO_tdmClockSourceMode and AIO_tdmClockSinkMode below)
```C++
AIO_tdmParameterAudioDataShiftBits: 7
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Number of bits to shift the TDM data (see AIO_tdmParameterAudioDataShiftEnabled above)
```C++
AIO_tdmParameterLogicLevel: 8
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sets the logic level for the TDM data; 0 - TDM data is active low, 1 - TDM data is active high
```C++
AIO_tdmParameterFSYNCPosition: 9
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 Bit parameter that sets the position for start of positive portion of FSYNC. Valid positions are 0
```C++
AIO_tdmParameterFSYNCWidth: 10
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 bit integer parameter that sets the bit position for the start of positive portion of FSYNC.
 Valid positions are 0 (first data bit position) through frame length - 1
 [clock source mode] bit 0 corresponds to the MSB of TDM output.
 [clock sink mode] bit 0 corresponds to the MSB of TDM input
### Clock mode settings for an AIO-T module

```C++
AIO_tdmClockSourceMode: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Clock source mode - FSYNC and SCLK are outputs
```C++
AIO_tdmClockSinkMode: 1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Clock sink mode - FSYNC and SCLK are inputs
AIO-T configuration constants and parameters
AIO device parameters for the entire AIO
### Global configuration parameters for the entire AIO

```C++
AIO_deviceParameterClockSource: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The audio clock source for the entire AIO
### Supported audio clock sources for the AIO

```C++
AIO_clockSourceInternal: 1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AIO internal clock generator
```C++
AIO_clockSourceUSB: 2
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Synchronize to USB start-of-frame
```C++
AIO_clockSourceCenterModule: 3
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Synchronize to center audio module
```C++
AIO_clockSourceOuterModule: 4
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Synchronize to outer audio module
AIO device parameters for the entire AIO
### Return values for API functions that return a status code

```C++
AIO_OK: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_OK if the function call was successful
```C++
AIO_notInitialized: -1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_notIntialized if the AIO library has not been initialized
```C++
AIO_invalidInputChannel: -2
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_invalidInputChannel if the input channel number is invalid
```C++
AIO_invalidOutputChannel: -3
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_invalidOutputChannel if the output channel number is invalid
```C++
AIO_invalidParameter: -4
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_invalidParameter if a parameter is invalid
```C++
AIO_invalidBufferSize: -5
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_invalidBufferSize if the buffer size is invalid
```C++
AIO_notFound: -6
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_notFound if the AIO is not found
```C++
AIO_usbCommandFailed: -7
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_usbCommandFailed if the USB command failed
```C++
AIO_invalidModuleSlot: -8
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_invalidModuleSlot if the module slot is invalid
```C++
AIO_notSupported: -9
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_notSupported if the function is not supported
```C++
AIO_tedsDeviceNotFound: -10
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_tedsDeviceNotFound if the TEDS device is not found
```C++
AIO_invalidValue: -11
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_invalidValue if the value is invalid
```C++
AIO_missingParameter: -12
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_missingParameter if a parameter is missing
```C++
AIO_timeout: -13
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_timeout if a timeout occurred
```C++
AIO_invalidPointer: -14
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Returns AIO_invalidPointer if a pointer is invalid
### Constant values and strings

```C++
AIO_notificationString: 0
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String for control change broadcast event
```C++
AIO_numModuleSlots: 2
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Number of audio module slots in an AIO chassis
