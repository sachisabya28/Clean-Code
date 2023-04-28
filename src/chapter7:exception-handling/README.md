# Exception Handling

## Use Exceptions Rather Than Return Codes

```
if (handle != DeviceHandle.INVALID):
    // Save the device status to the record field
    retrieveDeviceRecord(handle);
    // If not suspended, shut down
    if (record.getStatus() != DEVICE_SUSPENDED):
        pauseDevice(handle);
        clearDeviceWorkQueue(handle);
        closeDevice(handle);
    else:
        logger.log("Device suspended. Unable to shut down");
else:
    logger.log("Invalid handle for: " + DEV1.toString());
```

```
def sendShutDown():
    try:
        tryToShutDown();
    except DeviceShutDownError e:
        logger.log(e)


def tryToShutDown():
    try:
        DeviceHandle handle = getHandle(DEV1);
        DeviceRecord record = retrieveDeviceRecord(handle);
        pauseDevice(handle);
        clearDeviceWorkQueue(handle);
    except Exception:
        raise DeviceShutDownError
```

## Define Exception Classes in Terms of a Caller’s Needs

```
try
    port.open()
except (DeviceResponseException e):
    reportPortError(e);
    logger.log("Device response exception", e);
except (ATM1212UnlockedException e):
    reportPortError(e);
    logger.log("Unlock exception", e);
except (GMXError e):
    reportPortError(e)
    logger.log("Device response exception");
```

we know that the work that we are doing is roughly the same
regardless of the exception, we can simplify our code considerably by wrapping the API
that we are calling and making sure that it returns a common exception type:

```
LocalPort port = new LocalPort(12);
try:
    port.open()
except (PortDeviceFailure e):
    reportError(e);
    logger.log(e.getMessage(), e)
```

poor exception classification

```
try {
    port.open();
} catch (DeviceResponseException e) {
    reportPortError(e);
    logger.log("Device response exception", e);
} catch (ATM1212UnlockedException e) {
    reportPortError(e);
    logger.log("Unlock exception", e);
} catch (GMXError e) {
    reportPortError(e);
    logger.log("Device response exception");
finally {
    …
}
```
here we are doing is roughly the same
regardless of the exception, we can simplify our code considerably by wrapping the API
that we are calling and making sure that it returns a common exception type:

```
LocalPort port = new LocalPort(12);
try {
    port.open();
} catch (PortDeviceFailure e) {
    reportError(e);
    logger.log(e.getMessage(), e);
} finally {
…
}
```

## Don't return Null

In many cases, special case objects are an easy remedy. Imagine that you have code
like this:
```
employees = getEmployees();
if (employees != null) {
    for(Employee e : employees) {
    totalPay += e.getPay();
    }
}
```
Right now, getEmployees can return null, but does it have to? If we change getEmployee so
that it returns an empty list, we can clean up the code:
```
    List<Employee> employees = getEmployees();
    for(Employee e : employees) {
    totalPay += e.getPay();
}
```

