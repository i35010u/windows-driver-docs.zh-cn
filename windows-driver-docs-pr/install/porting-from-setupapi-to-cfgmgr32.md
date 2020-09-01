---
title: 将代码从 SetupApi 移植到 CfgMgr32
description: 本主题提供了一些代码示例，这些示例演示如何将使用 Setupapi.dll 功能的代码移植到使用 Cfgmgr32.dll。
ms.assetid: 36668A17-EA56-464C-A38B-C75BE2359412
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb4aa94438050f03e8b0b3d4df9d86be89620328
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096029"
---
# <a name="porting-code-from-setupapi-to-cfgmgr32"></a>将代码从 SetupApi 移植到 CfgMgr32


本主题提供了一些代码示例，这些示例演示如何将使用 Setupapi.dll 功能的代码移植到使用 Cfgmgr32.dll。 通过迁移你的代码，你可以在通用 Windows 平台 (UWP) 上运行你的代码，此功能不支持 Setupapi.log。 UWP 支持 CfgMgr32 的子集，特别是通过 api 集公开的功能 `api-ms-win-devices-config-l1-1-0.dll` (Windows 8 及更高版本) 或 `api-ms-win-devices-config-l1-1-1.dll` (Windows 8.1 和更) 高版本的 api 集。 在 Windows 10 和更高版本中，只需链接到即可 `onecore.lib` 。

若要查看上述 API 集中的函数列表，请参阅 [WINDOWS Api 集](/windows/desktop/apiindex/windows-apisets) 或 [Onecore： api-ms-win-devices-config-l1-1-1.dll](/windows/desktop/apiindex/umbrella-lib-onecore#_api-ms-win-devices-config-l1-1-1.dll)中的 api。

以下部分包含应用程序通常使用的代码示例。

-   [获取现有设备的列表并检索每个设备的属性](#get-a-list-of-present-devices-and-retrieve-a-property-for-each-device)
-   [获取接口的列表，获取设备，公开每个接口，并从设备获取属性](#get-a-list-of-interfaces-get-the-device-exposing-each-interface-and-get-a-property-from-the-device)
-   [从特定设备获取属性](#get-a-property-from-a-specific-device)
-   [禁用设备](#disable-device)
-   [启用设备](#enable-device)
-   [重启设备](#restart-device)

## <a name="get-a-list-of-present-devices-and-retrieve-a-property-for-each-device"></a>获取现有设备的列表并检索每个设备的属性


此示例使用 [**SetupDiGetClassDevs**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw) 获取所有当前设备的列表，并循环访问它们以检索每个设备的设备说明。

```ManagedCPlusPlus
VOID
GetDevicePropertiesSetupapi(
    VOID
    )
{
    HDEVINFO DeviceInfoSet = INVALID_HANDLE_VALUE;
    SP_DEVINFO_DATA DeviceInfoData;
    DWORD Index;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;

    DeviceInfoSet = SetupDiGetClassDevs(NULL,
                                        NULL,
                                        NULL,
                                        DIGCF_ALLCLASSES | DIGCF_PRESENT);

    if (DeviceInfoSet == INVALID_HANDLE_VALUE)
    {
        goto Exit;
    }

    ZeroMemory(&DeviceInfoData, sizeof(DeviceInfoData));
    DeviceInfoData.cbSize = sizeof(DeviceInfoData);

    for (Index = 0;
         SetupDiEnumDeviceInfo(DeviceInfoSet,
                               Index,
                               &DeviceInfoData);
         Index++)
    {
        // Query a property on the device.  For example, the device description.
        if (!SetupDiGetDeviceProperty(DeviceInfoSet,
                                      &DeviceInfoData,
                                      &DEVPKEY_Device_DeviceDesc,
                                      &PropertyType,
                                      (PBYTE)DeviceDesc,
                                      sizeof(DeviceDesc),
                                      NULL,
                                      0))
        {
            // The error can be retrieved with GetLastError();
            continue;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            continue;
        }
    }

    if (GetLastError() != ERROR_NO_MORE_ITEMS)
    {
        goto Exit;
    }

  Exit:

    if (DeviceInfoSet != INVALID_HANDLE_VALUE)
    {
        SetupDiDestroyDeviceInfoList(DeviceInfoSet);
    }

    return;
}
```

此示例使用 [**CM_Get_Device_ID_List**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_lista) 获取现有设备的列表，并循环访问它们以检索每个设备的设备说明。

```ManagedCPlusPlus
VOID
GetDevicePropertiesCfgmgr32(
    VOID
    )
{
    CONFIGRET cr = CR_SUCCESS;
    PWSTR DeviceList = NULL;
    ULONG DeviceListLength = 0;
    PWSTR CurrentDevice;
    DEVINST Devinst;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;
    ULONG PropertySize;
    DWORD Index = 0;

    cr = CM_Get_Device_ID_List_Size(&DeviceListLength,
                                    NULL,
                                    CM_GETIDLIST_FILTER_PRESENT);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    DeviceList = (PWSTR)HeapAlloc(GetProcessHeap(),
                                  HEAP_ZERO_MEMORY,
                                  DeviceListLength * sizeof(WCHAR));

    if (DeviceList == NULL) {
        goto Exit;
    }

    cr = CM_Get_Device_ID_List(NULL,
                               DeviceList,
                               DeviceListLength,
                               CM_GETIDLIST_FILTER_PRESENT);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    for (CurrentDevice = DeviceList;
         *CurrentDevice;
         CurrentDevice += wcslen(CurrentDevice) + 1)
    {

        // If the list of devices also includes non-present devices,
        // CM_LOCATE_DEVNODE_PHANTOM should be used in place of
        // CM_LOCATE_DEVNODE_NORMAL.
        cr = CM_Locate_DevNode(&Devinst,
                               CurrentDevice,
                               CM_LOCATE_DEVNODE_NORMAL);

        if (cr != CR_SUCCESS)
        {
            goto Exit;
        }

        // Query a property on the device.  For example, the device description.
        PropertySize = sizeof(DeviceDesc);
        cr = CM_Get_DevNode_Property(Devinst,
                                     &DEVPKEY_Device_DeviceDesc,
                                     &PropertyType,
                                     (PBYTE)DeviceDesc,
                                     &PropertySize,
                                     0);

        if (cr != CR_SUCCESS)
        {
            Index++;
            continue;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            Index++;
            continue;
        }

        Index++;
    }

  Exit:

    if (DeviceList != NULL)
    {
        HeapFree(GetProcessHeap(),
                 0,
                 DeviceList);
    }

    return;
}
```

## <a name="get-a-list-of-interfaces-get-the-device-exposing-each-interface-and-get-a-property-from-the-device"></a>获取接口的列表，获取设备，公开每个接口，并从设备获取属性


此示例使用 [**SetupDiGetClassDevs**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)获取类 GUID_DEVINTERFACE_VOLUME 中所有接口的列表。 对于每个接口，它会获取公开接口的设备并获取该设备的属性。

```ManagedCPlusPlus
VOID
GetInterfacesAndDevicePropertySetupapi(
    VOID
    )
{
    HDEVINFO DeviceInfoSet = INVALID_HANDLE_VALUE;
    SP_DEVICE_INTERFACE_DATA DeviceInterfaceData;
    SP_DEVINFO_DATA DeviceInfoData;
    DWORD Index;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;

    DeviceInfoSet = SetupDiGetClassDevs(&GUID_DEVINTERFACE_VOLUME,
                                        NULL,
                                        NULL,
                                        DIGCF_DEVICEINTERFACE);

    if (DeviceInfoSet == INVALID_HANDLE_VALUE)
    {
        goto Exit;
    }

    ZeroMemory(&DeviceInterfaceData, sizeof(DeviceInterfaceData));
    DeviceInterfaceData.cbSize = sizeof(DeviceInterfaceData);

    for (Index = 0;
         SetupDiEnumDeviceInterfaces(DeviceInfoSet,
                                     NULL,
                                     &GUID_DEVINTERFACE_VOLUME,
                                     Index,
                                     &DeviceInterfaceData);
         Index++)
    {

        ZeroMemory(&DeviceInfoData, sizeof(DeviceInfoData));
        DeviceInfoData.cbSize = sizeof(DeviceInfoData);

        if ((!SetupDiGetDeviceInterfaceDetail(DeviceInfoSet,
                                              &DeviceInterfaceData,
                                              NULL,
                                              0,
                                              NULL,
                                              &DeviceInfoData)) &&
            (GetLastError() != ERROR_INSUFFICIENT_BUFFER))
        {
            // The error can be retrieved with GetLastError();
            goto Exit;
        }

        // Query a property on the device.  For example, the device description.
        if (!SetupDiGetDeviceProperty(DeviceInfoSet,
                                      &DeviceInfoData,
                                      &DEVPKEY_Device_DeviceDesc,
                                      &PropertyType,
                                      (PBYTE)DeviceDesc,
                                      sizeof(DeviceDesc),
                                      NULL,
                                      0))
        {
            // The error can be retrieved with GetLastError();
            goto Exit;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            goto Exit;
        }
    }

    if (GetLastError() != ERROR_NO_MORE_ITEMS)
    {
        goto Exit;
    }

  Exit:

    if (DeviceInfoSet != INVALID_HANDLE_VALUE)
    {
        SetupDiDestroyDeviceInfoList(DeviceInfoSet);
    }

    return;
}
```

此示例使用 [**CM_Get_Device_Interface_List**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista)获取类 GUID_DEVINTERFACE_VOLUME 中所有接口的列表。 对于每个接口，它会获取公开接口的设备并获取该设备的属性。

```ManagedCPlusPlus
VOID
GetInterfacesAndDevicePropertyCfgmgr32(
    VOID
    )
{
    CONFIGRET cr = CR_SUCCESS;
    PWSTR DeviceInterfaceList = NULL;
    ULONG DeviceInterfaceListLength = 0;
    PWSTR CurrentInterface;
    WCHAR CurrentDevice[MAX_DEVICE_ID_LEN];
    DEVINST Devinst;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;
    ULONG PropertySize;
    DWORD Index = 0;

    do {
        cr = CM_Get_Device_Interface_List_Size(&DeviceInterfaceListLength,
                                               (LPGUID)&GUID_DEVINTERFACE_VOLUME,
                                               NULL,
                                               CM_GET_DEVICE_INTERFACE_LIST_ALL_DEVICES);

        if (cr != CR_SUCCESS)
        {
            break;
        }

        if (DeviceInterfaceList != NULL) {
            HeapFree(GetProcessHeap(),
                     0,
                     DeviceInterfaceList);
        }

        DeviceInterfaceList = (PWSTR)HeapAlloc(GetProcessHeap(),
                                               HEAP_ZERO_MEMORY,
                                               DeviceInterfaceListLength * sizeof(WCHAR));

        if (DeviceInterfaceList == NULL)
        {
            cr = CR_OUT_OF_MEMORY;
            break;
        }

        cr = CM_Get_Device_Interface_List((LPGUID)&GUID_DEVINTERFACE_VOLUME,
                                          NULL,
                                          DeviceInterfaceList,
                                          DeviceInterfaceListLength,
                                          CM_GET_DEVICE_INTERFACE_LIST_ALL_DEVICES);
    } while (cr == CR_BUFFER_SMALL);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    for (CurrentInterface = DeviceInterfaceList;
         *CurrentInterface;
         CurrentInterface += wcslen(CurrentInterface) + 1)
    {

        PropertySize = sizeof(CurrentDevice);
        cr = CM_Get_Device_Interface_Property(CurrentInterface,
                                              &DEVPKEY_Device_InstanceId,
                                              &PropertyType,
                                              (PBYTE)CurrentDevice,
                                              &PropertySize,
                                              0);

        if (cr != CR_SUCCESS)
        {
            goto Exit;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            goto Exit;
        }

        // Since the list of interfaces includes all interfaces, enabled or not, the
        // device that exposed that interface may currently be non-present, so
        // CM_LOCATE_DEVNODE_PHANTOM should be used.
        cr = CM_Locate_DevNode(&Devinst,
                               CurrentDevice,
                               CM_LOCATE_DEVNODE_PHANTOM);

        if (cr != CR_SUCCESS)
        {
            goto Exit;
        }

        // Query a property on the device.  For example, the device description.
        PropertySize = sizeof(DeviceDesc);
        cr = CM_Get_DevNode_Property(Devinst,
                                     &DEVPKEY_Device_DeviceDesc,
                                     &PropertyType,
                                     (PBYTE)DeviceDesc,
                                     &PropertySize,
                                     0);

        if (cr != CR_SUCCESS)
        {
            goto Exit;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            goto Exit;
        }

        Index++;
    }

  Exit:

    if (DeviceInterfaceList != NULL)
    {
        HeapFree(GetProcessHeap(),
                 0,
                 DeviceInterfaceList);
    }

    return;
}
```

## <a name="get-a-property-from-a-specific-device"></a>从特定设备获取属性


此示例使用特定设备的设备实例路径，并使用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)从该路径中检索属性。

```ManagedCPlusPlus
VOID
GetDevicePropertySpecificDeviceSetupapi(
    VOID
    )
{
    HDEVINFO DeviceInfoSet = INVALID_HANDLE_VALUE;
    SP_DEVINFO_DATA DeviceInfoData;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;

    DeviceInfoSet = SetupDiCreateDeviceInfoList(NULL, NULL);

    if (DeviceInfoSet == INVALID_HANDLE_VALUE)
    {
        goto Exit;
    }

    ZeroMemory(&DeviceInfoData, sizeof(DeviceInfoData));
    DeviceInfoData.cbSize = sizeof(DeviceInfoData);

    if (!SetupDiOpenDeviceInfo(DeviceInfoSet,
                               MY_DEVICE,
                               NULL,
                               0,
                               &DeviceInfoData))
    {
        // The error can be retrieved with GetLastError();
        goto Exit;
    }

    // Query a property on the device.  For example, the device description.
    if (!SetupDiGetDeviceProperty(DeviceInfoSet,
                                  &DeviceInfoData,
                                  &DEVPKEY_Device_DeviceDesc,
                                  &PropertyType,
                                  (PBYTE)DeviceDesc,
                                  sizeof(DeviceDesc),
                                  NULL,
                                  0)) {
        // The error can be retrieved with GetLastError();
        goto Exit;
    }

    if (PropertyType != DEVPROP_TYPE_STRING)
    {
        goto Exit;
    }

  Exit:

    if (DeviceInfoSet != INVALID_HANDLE_VALUE)
    {
        SetupDiDestroyDeviceInfoList(DeviceInfoSet);
    }

    return;
}
```

此示例使用特定设备的设备实例路径，并使用 [**CM_Get_DevNode_Property**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_propertyw)从该路径中检索属性。

```ManagedCPlusPlus
void
GetDevicePropertySpecificDeviceCfgmgr32(
    VOID
    )
{
    CONFIGRET cr = CR_SUCCESS;
    DEVINST Devinst;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;
    ULONG PropertySize;

    // If MY_DEVICE could be a non-present device, CM_LOCATE_DEVNODE_PHANTOM
    // should be used in place of CM_LOCATE_DEVNODE_NORMAL.
    cr = CM_Locate_DevNode(&Devinst,
                           MY_DEVICE,
                           CM_LOCATE_DEVNODE_NORMAL);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    // Query a property on the device.  For example, the device description.
    PropertySize = sizeof(DeviceDesc);
    cr = CM_Get_DevNode_Property(Devinst,
                                 &DEVPKEY_Device_DeviceDesc,
                                 &PropertyType,
                                 (PBYTE)DeviceDesc,
                                 &PropertySize,
                                 0);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    if (PropertyType != DEVPROP_TYPE_STRING)
    {
        goto Exit;
    }

  Exit:

    return;
}
```

## <a name="disable-device"></a>禁用设备


此示例演示如何使用 CfgMgr32 禁用设备。 若要使用 Setupapi.log 执行此操作，请将 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) 与 *InstallFunction* 的 **DIF_PROPERTYCHANGE**一起使用，并指定 **DICS_DISABLE**。

**注意**   默认情况下，调用 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) 会导致设备在重新启动时始终处于禁用状态。 若要在调用 [**CM_Disable_DevNode**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_disable_devnode)时跨重新启动禁用设备，则必须指定 **CM_DISABLE_PERSIST** 标志。



```ManagedCPlusPlus
    cr = CM_Locate_DevNode(&devinst,
                           (DEVINSTID_W)DeviceInstanceId,
                           CM_LOCATE_DEVNODE_NORMAL);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }

    cr = CM_Disable_DevNode(devinst, 0);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }
```

## <a name="enable-device"></a>启用设备


此示例演示如何使用 CfgMgr32 启用设备。 若要使用 Setupapi.log 执行此操作，请将 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) 与 *InstallFunction* 的 **DIF_PROPERTYCHANGE**一起使用，并指定 **DICS_ENABLE**。

```ManagedCPlusPlus
    cr = CM_Locate_DevNode(&devinst,
                           (DEVINSTID_W)DeviceInstanceId,
                           CM_LOCATE_DEVNODE_NORMAL);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }

    cr = CM_Enable_DevNode(devinst, 0);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }
```

## <a name="restart-device"></a>重启设备


此示例演示如何使用 CfgMgr32 重新启动设备。 若要使用 Setupapi.log 执行此操作，请将 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) 与 *InstallFunction* 的 **DIF_PROPERTYCHANGE**一起使用，并指定 **DICS_PROPCHANGE**。

```ManagedCPlusPlus
    cr = CM_Locate_DevNode(&devinst,
                           (DEVINSTID_W)DeviceInstanceId,
                           CM_LOCATE_DEVNODE_NORMAL);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }

    cr = CM_Query_And_Remove_SubTree(devinst,
                                     NULL,
                                     NULL,
                                     0,
                                     CM_REMOVE_NO_RESTART);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }

    cr = CM_Setup_DevNode(devinst,
                          CM_SETUP_DEVNODE_READY);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }
```