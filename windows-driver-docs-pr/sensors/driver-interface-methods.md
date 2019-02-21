---
title: 驱动程序接口方法
ms.assetid: 675F4188-3B9A-421B-98EF-FE063B550231
description: 接口由传感器驱动程序支持的方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b279db64e2a4be7f99b5bd43ef25186d7ce9917b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525970"
---
# <a name="driver-interface-methods"></a>驱动程序接口方法


传感器驱动程序必须支持传感器平台的设备驱动程序接口 (DDI)。 伪代码演示了这可以通过使用以下方法：

-   DDIOnClientConnect(sensorID, clientID)
-   DDIOnClientDisconnect(sensorID, clientID)
-   DDIOnClientSubscribeToEvents(sensorID, clientID)
-   DDIOnClientUnsubscribeFromEvents(sensorID, clientID)
-   DDIOnSetCRI （sensorID，requestedCRI）
-   DDIOnSetCS （sensorID，requestedCSs）
-   DDIOnSetLDA （sensorID，requestedLDA）
-   DDIOnGetProperties(sensorID, CRI, CS\[\], LDA)
-   DDIOnGetDatafields(sensorID, datafields\[\])
-   DDIHandleAsyncDataEvent （sensorID，inputReport）

## <a name="client-connections"></a>客户端连接


**DDIOnClientConnect**并**DDIOnClientDisonnect**方法演示如何将驱动程序处理的连接和断开连接的客户端。

```cpp
DDIOnClientConnect(sensorID, clientID)
{
    clientList[clientID] = clientEntry

    clientEntry.clientCRI = DONT_CARE
    clientEntry.clientCS[] = default[]
    clientEntry.clientLDA = default //location only
    clientList[clientID] = clientEntry
    clientCount++

    if (1 == clientCount)
    {
        DriverUpdateDeviceState()
        DriverUpdateSensorState(sensorID
        DriverUpdateDatafields(sensorID)
        effectiveRS = DriverUpdateRS(sensorID)
        effectivePS = DriverUpdatePS(sensorID)
}
    else //more than 1 client connected
    {
        //no additional initial action required
    }

    // Since a new client has connected, the effective CRI, CS[], and LDA must
    // be re-evaluated for all of the clients now connected
    effectiveCRI = DriverUpdateCRI(sensorID)
    effectiveCS[] = DriverUpdateCS(sensorID)
    effectiveLDA = DriverUpdateLDA(sensorID) //location only
    effectiveRS = DriverUpdateRS(sensorID)
    effectivePS = DriverUpdatePS(sensorID)
}
```

```cpp
DDIOnClientDisconnect(sensorID, clientID)
{
    delete clientList[clientID]
    clientCount--

    if (0 == clientCount)
    {
        DriverUpdateSensorState(sensorID)
        DriverUpdateDatafields(sensorID)
        DriverUpdateDeviceState()

        flagCRI = false
        flagCS = false
    }
    else //clients are still connected
    {
        // A client has NOT specified a CRI if
        // - the CRI has never been set by that client since having been connected
        // - the client has specified a CRI of ‘0’, which means to use the default
        if (no remaining client has specified CRI)
        {
            flagCRI = false
        }
        // A client has NOT specified a CS[] if
        // - the CS[] has never been set by that client since having been connected
        // If the client HAS specified a CS[], there is no way for the client to
        // instead revert to the default (as can be done with the CRI)
        if (no remaining client has specified CS[])
        {
            flagCS = false
        }
    }

    // Since an existing client has disconnected, the effective CRI, CS[], and LDA must
    // be re-evaluated for all of the clients now connected
    effectiveCRI = DriverUpdateCRI(sensorID)
    effectiveCS[] = DriverUpdateCS(sensorID)
    effectiveLDA = DriverUpdateLDA(sensorID) //location only
    effectiveRS = DriverUpdateRS(sensorID)
    effectivePS = DriverUpdatePS(sensorID)
}
```

## <a name="client-event-subscriptions"></a>客户端事件订阅


**DDIOnClientSubscribeToEvents**并**DDIOnClientUnsubscribeFromEvents**方法演示如何将驱动程序处理的事件订阅。

```cpp
DDIOnClientSubscribeToEvents(sensorID, clientID)
{
    clientList[clientID].clientSubscribed = true
    subscriberCount++

    if (1 == subscriberCount)
    {
        DriverUpdateSensorState(sensorID, sensorStateActive, reportingStateAllEvents)
    }
    else //more than 1 subscriber connected
    {
        //no additional initial action required
    }

    effectiveRS = DriverUpdateRS(sensorID)
    effectivePS = DriverUpdatePS(sensorID)
}
```

```cpp
DDIOnClientUnsubscribeFromEvents(sensorID, clientID)
{
    delete clientList[clientID]
    subscriberCount--

    if (0 == subscriberCount)
    {
        DriverUpdateSensorState(sensorID
    }
    else //clients are still subscribed
    {
        effectiveRS = DriverUpdateRS(sensorID)
        effectivePS = DriverUpdatePS(sensorID)
    }
}
```

## <a name="sensor-reporting-fields"></a>传感器进行报告的字段


**DDIOnSetCRI**， **DDIOnSetCS**，并**DDIOnSetLDA**方法演示如何将驱动程序设置当前报告间隔、 变化敏感度和位置数据的准确性字段。

```cpp
/////////////////////////////////////////////////////////////////////////////////////////////
//
// DDIOnSetCRI
//
// Note that setting the CRI has an effect on the reportingState at the device because by setting
// the CRI the client implies it wants event-driven data constantly available in the datafields
// even though that client has not subscribed to events.
//
/////////////////////////////////////////////////////////////////////////////////////////////
DDIOnSetCRI(sensorID, clientID, requestedCRI) //OnSetProperties
{
    if (requestedCRI == DONT_CARE)
    {
        if (clientList[clientID].clientCRI != DONT_CARE)
        {
             clientList[clientID].clientCRI = DONT_CARE
        }
        // A client has NOT specified a CRI if
        // - the CRI has never been set by that client since having been connected
        // - the client has specified a CRI of ‘0’, which means to use the default
        if (no remaining client has specified CRI)
        {
            flagCRI = false
        }
    }
    else
    {
        //this sets the value of CRI to a definite value
        clientList[clientID].clientCRI = requestedCRI
        flagCRI = true
    }

    DriverUpdateCRI(sensorID)
    DriverUpdateSensorState(sensorID)
}
```

```cpp
/////////////////////////////////////////////////////////////////////////////////////////////
//
// DDIOnSetCS
//
// Note that setting the CS for any datafield only has an effect on the CS at the device and
// has no explicit effect on either the reporting state (eventing) or the power state.
// However, the device may wish to take into account the CS setting when managing power
//
/////////////////////////////////////////////////////////////////////////////////////////////
DDIOnSetCS(sensorID, clientID, requestedCS[]) //OnSetProperties
{
    for (each datafield n supported by sensorID)
    {
        if (requestedCS[n] == DONT_CARE)
        {
            if (clientList[clientID].clientCS[n] != DONT_CARE)
            {
                 clientList[clientID].clientCS[n] = DONT_CARE
            }
            // A client has NOT specified a CS for datafield n if
            // - the CS[n] has never been set by that client since having been connected
            // - the client has specified a CS[n] of type ‘VT_NULL’, which means to use the default
            if (no remaining client has specified CRI)
            {
                flagCS = false
            }
        }
        else
        {
            //this sets the value of CS[n] to a definite value
            clientList[clientID].clientCS[n] = requestedCS
            flagCS = true
        }
    }

    DriverUpdateCS(sensorID)
}
```

```cpp
DDIOnSetLDA(sensorID, clientID, requestedLDA) //OnSetProperties, location only
{
    clientList[clientID].clientLDA = requestedLDA

    DriverUpdateLDA(sensorID)
}
```

## <a name="property-and-datafield-retrieval"></a>属性和数据字段检索


**DDIOnGetProperties**并**DDIOnGetDatafields**方法演示如何将驱动程序中检索属性和 datafields。

```cpp
DDIOnGetProperties(sensorID, CRI, CS[], LDA)
{
    // the following properties can be set from the API
    CRI = effectiveCRI
    CS[] = effectiveCS[]
    LDA = effective[LDA]

    // the following properties cannot be set from the API
    // the driver provides defaults for these properties
    // the defaults can be overridden by the device
    sensorCategory = effectiveSensorCategory
    sensorType = effectiveSensorType
    minCRI = effectiveMinCRI
    persistentUniqueID = effectivePersistentUniqueID
    sensorManufacturer = effectiveSensorManufacturer
    sensorModel = effectiveSensorModel
    serialNumber = effectiveSerialNumber
    friendlyName = effectiveFriendlyName
    sensorDescription = effectiveDescription
    connectionType = effectiveConnectionType
}
```

```cpp
DDIOnGetDatafields(sensorID, datafields[])
{
    if (((false == flagCRI) && (0 == subscriberCount)) || (false == initalDataReceived))
    {
        //poll sensorID device for data
        DriverUpdateDatafields(sensorID)

        //wait for poll response for no more than pollResponseTimeLimit
        if (response received from poll)
        {
            datafields[] = currentDatafields[]
        }
        Else //no response was received within pollResponseTimeLimit mS
        {
            if (true == initialDataReceived)
            {
                datafields[] = currentDatafields[] //not updated
            }
            else
            {
                datafields[] = currentDatafields[] //are VT_EMPTY
            }
        }
    }
    else
    {
        datafields[] = currentDatafields[] //updated at effectiveCRI rate
    }
}
```

## <a name="supporting-asynchronous-events"></a>支持异步事件


**DDIHandleAsyncDataEvent**方法演示了如何将驱动程序支持异步事件。

```cpp
DDIHandleAsyncDataEvent(sensorID, buffer)
{
    if (buffer.sensorDeviceState == sensorStateReady)
    {
        if (buffer.sensorDeviceEvent == eventTypeCS)
        {
            initialDataReceived = true
        }
        else if (buffer.sensorDeviceEvent == eventTypeDataPoll)
        {
            initialDataReceived = true
            pollResponseReceived = true
        }

        currentDatafields[] = buffer[]
        SetState(sensorStateReady)
        Fire Event
    }
    else
    {
        Set received initial data = false
        SetState(buffer.sensorDeviceState) //something other than ready
        currentDatafields[] = VT_EMPTY
    }
}
```

## <a name="related-topics"></a>相关主题
[传感器驱动程序开发的基础知识](sensor-driver-development-basics.md)



