---
title: 编码器代码示例
description: 编码器代码示例
ms.assetid: cbe773ad-2222-4d62-8e1e-6d47418a3e7c
keywords:
- 可变比特率 WDK 编码器
- 编码器设备 WDK AVStream
- AVStream WDK，编码器设备
- 未压缩的数据流 WDK AVStream
- 编码流 WDK AVStream
- 音频编码器设备 WDK AVStream
- 视频编码器设备 WDK AVStream
- ENCAPIPARAM_BITRATE_MODE
- ENCAPIPARAM_BITRATE
- 比特率 WDK 编码器
- 注册表 WDK 编码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b781f40bf5e1514701fd6e55c0af9c68b1e447
ms.sourcegitcommit: b481c9513a9ea7f824ecabd1ae18876548032252
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879035"
---
# <a name="encoder-code-examples"></a>编码器代码示例

下面的代码示例基于[AVStream 模拟硬件示例驱动程序（AVSHwS）](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)。 它们演示了以下内容：

- 如何指定编码器支持的比特率

- 如何指定编码器支持的比特率编码模式

- 如何在运行时指定编码器设备的*设备参数 \\ 功能*注册表项下的元数据值

## <a name="implementing-supported-bit-rates"></a>实现支持的比特率

下面的代码段演示如何实现对[ENCAPIPARAM \_ 比特率](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate)属性的支持。 使用[**KSPROPERTY \_ 单步 \_ 长**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)结构来指定400位/秒（bps）的单步执行粒度，使用 400-bps 下限和 4000000-bps 上限。

```cpp
const KSPROPERTY_STEPPING_LONG BitRateRanges [] = {
    {
        400,
        0,
        400,
        4000000
    }
};
```

如果通过右键单击工具（如 GraphEdit）中的筛选器来访问编码器筛选器的属性页，将看到使用这些值的**比特率**滑块条。

接下来，在创建编码器筛选器的实例时，指定其默认编码比特率。 请注意，所使用的数据类型为 ULONG，对应于 ENCAPIPARAM 比特率属性所需的属性值类型 \_ 。 此值是在编码器的属性页中显示的默认编码 "比特率"：

```cpp
const ULONG BitRateValues [] = {
    1000000
};
```

指定合法范围列表和 ENCAPIPARAM \_ 比特率属性的默认值：

```cpp
 const KSPROPERTY_MEMBERSLIST BitRateMembersList [] = {
    {
        {
            KSPROPERTY_MEMBER_STEPPEDRANGES,
            sizeof (BitRateRanges),
            SIZEOF_ARRAY (BitRateRanges),
            0
        },
        BitRateRanges
    },
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateValues),
            SIZEOF_ARRAY (BitRateValues),
            KSPROPERTY_MEMBER_FLAG_DEFAULT
        },
        BitRateValues
    }
};
```

```cpp
 const KSPROPERTY_VALUES BitRateValuesSet = {
    {
        STATICGUIDOF (KSPROPTYPESETID_General),
        VT_UI4,
        0
    },
    SIZEOF_ARRAY (BitRateMembersList),
    BitRateMembersList
};
```

指定为 ENCAPIPARAM \_ 比特率属性集定义的单个属性：

```cpp
DEFINE_KSPROPERTY_TABLE(ENCAPI_BitRate) {
    DEFINE_KSPROPERTY_ITEM (
        0,
        GetBitRateHandler, //Get-property handler supported
        sizeof (KSPROPERTY),
        sizeof (ULONG),
        SetBitRateHandler, //Set-property handler supported
        &BitRateValuesSet,
        0,
        NULL,
        NULL,
        sizeof (ULONG)
        )
};
```

> [!NOTE]
> *Get*属性处理程序返回编码比特率，并且*设置*属性处理程序必须先测试传入传入的值是否有效，然后再使用它。

## <a name="implementing-supported-encoding-bit-rate-modes"></a>实现支持的编码比特率模式

下面的代码段演示如何实现对[ENCAPIPARAM \_ 比特率 \_ 模式](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate-mode)属性的支持。

定义编码器支持的编码模式：

```cpp
 const VIDEOENCODER_BITRATE_MODE BitRateModeValues [] = {
    ConstantBitRate,
    VariableBitRateAverage
};
```

指定默认编码比特率模式，即平均可变比特率：

```cpp
const VIDEOENCODER_BITRATE_MODE BitRateModeDefaultValues [] = {
    VariableBitRateAverage
};
```

为 "ENCAPIPARAM" \_ 比特率模式属性指定合法范围和默认值的列表 \_ ：

```cpp
const KSPROPERTY_MEMBERSLIST BitRateModeMembersList [] = {
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateModeValues),
            SIZEOF_ARRAY (BitRateModeValues),
            0
        },
        BitRateModeValues
    },
    {
        {
            KSPROPERTY_MEMBER_VALUES,
            sizeof (BitRateModeDefaultValues),
            SIZEOF_ARRAY (BitRateModeDefaultValues),
            KSPROPERTY_MEMBER_FLAG_DEFAULT
        },
        BitRateModeDefaultValues
    }
};

const KSPROPERTY_VALUES BitRateModeValuesSet = {
    {
        STATICGUIDOF (KSPROPTYPESETID_General),
        VT_I4,
        0
    },
    SIZEOF_ARRAY (BitRateModeMembersList),
    BitRateModeMembersList
};
```

指定为 ENCAPIPARAM \_ 比特率模式属性集定义的单个属性 \_ ：

```cpp
DEFINE_KSPROPERTY_TABLE(ENCAPI_BitRateMode) {
    DEFINE_KSPROPERTY_ITEM (
        0,
        GetBitRateModeHandler, //Get-property handler supported
        sizeof (KSPROPERTY),
        sizeof (VIDEOENCODER_BITRATE_MODE),
        SetBitRateModeHandler, //Set-property handler supported
        &BitRateModeValuesSet,
        0,
        NULL,
        NULL,
        sizeof (VIDEOENCODER_BITRATE_MODE)
        )
};
```

> [!NOTE]
> *Get*属性处理程序应返回编码比特率模式，*并且在使用*传入的传入值之前必须先测试该传入传入的值是否有效。

然后，将属性集指定为[**KSFILTER \_ 描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构的自动化表。

```cpp
DEFINE_KSPROPERTY_SET_TABLE(PropertyTable) {
    DEFINE_KSPROPERTY_SET(
        &ENCAPIPARAM_BITRATE_MODE,
        SIZEOF_ARRAY (ENCAPI_BitRateMode),
        ENCAPI_BitRateMode,
        0,
        NULL
        ),
    DEFINE_KSPROPERTY_SET(
        &ENCAPIPARAM_BITRATE,
        SIZEOF_ARRAY (ENCAPI_BitRate),
        ENCAPI_BitRate,
        0,
        NULL
        )
};

DEFINE_KSAUTOMATION_TABLE(FilterTestTable) {
    DEFINE_KSAUTOMATION_PROPERTIES(PropertyTable),
    DEFINE_KSAUTOMATION_METHODS_NULL,
    DEFINE_KSAUTOMATION_EVENTS_NULL
};

const
KSFILTER_DESCRIPTOR
FilterDescriptor = {
    ...,
    &FilterTestTable, // Automation Table
    ...,
    ...
};
```

## <a name="specifying-the-encoders-capabilities-in-the-registry"></a>在注册表中指定编码器的功能

下面的代码示例演示如何在*Device Parameters*注册表项下创建*功能*注册表项，以及如何创建和指定*功能*项下的子项和值。 当驱动程序初始化时执行此代码。

> [!NOTE]
> 以下代码假设每个物理设备上存在单个硬件编码器。 如果你的硬件包含多个编码器，则必须循环访问**IoGetDeviceInterfaces**函数的调用中返回的列表，并为每个编码器注册功能。

```cpp
/**************************************************************************
CreateDwordValueInCapabilityRegistry()

IN Pdo: PhysicalDeviceObject
IN categoryGUID: Category GUID eg KSCATEGORY_CAPTURE

1. Get Symbolic name for interface
2. Open registry key for storing information about a
   particular device interface instance
3. Create Capabilities key under "Device Parameters" key
4. Create a DWORD value "TestCapValueDWORD" under Capabilities

Must be running at IRQL = PASSIVE_LEVEL in the context of a system thread
**************************************************************************/
NTSTATUS CreateDwordValueInCapabilityRegistry(IN PDEVICE_OBJECT pdo, IN GUID categoryGUID)

{

    // 1. Get Symbolic name for interface
    // pSymbolicNameList can contain multiple strings if pdo is NULL.
    // Driver should parse this list of string to get
    // the one corresponding to current device interface instance.
    PWSTR  pSymbolicNameList = NULL;

    NTSTATUS ntStatus = IoGetDeviceInterfaces(
        &categoryGUID,
        pdo,
        DEVICE_INTERFACE_INCLUDE_NONACTIVE,
        &pSymbolicNameList);
    if (NT_SUCCESS(ntStatus) && (NULL != pSymbolicNameList))
    {
        HANDLE hDeviceParametersKey = NULL;
        UNICODE_STRING symbolicName;

        // 2. Open registry key for storing information about a
        // particular device interface instance
        RtlInitUnicodeString(&symbolicName, pSymbolicNameList);
        ntStatus = IoOpenDeviceInterfaceRegistryKey(
            &symbolicName,
            KEY_READ|KEY_WRITE,
            &hDeviceParametersKey);
        if (NT_SUCCESS(ntStatus))
        {
            OBJECT_ATTRIBUTES objAttribSubKey;
            UNICODE_STRING subKey;

            // 3. Create Capabilities key under "Device Parameters" key
            RtlInitUnicodeString(&subKey,L"Capabilities");
            InitializeObjectAttributes(&objAttribSubKey,
                &subKey,
                OBJ_KERNEL_HANDLE,
                hDeviceParametersKey,
                NULL);

            HANDLE hCapabilityKeyHandle = NULL;

            ntStatus = ZwCreateKey(&hCapabilityKeyHandle,
                    KEY_READ|KEY_WRITE|KEY_SET_VALUE,
                    &objAttribSubKey,
                    0,
                    NULL,
                    REG_OPTION_NON_VOLATILE,
                    NULL);
            if (NT_SUCCESS(ntStatus))
            {
                OBJECT_ATTRIBUTES objAttribDwordKeyVal;
                UNICODE_STRING subValDword;

                // 4. Create a DWORD value "TestCapValueDWORD" under Capabilities
                RtlInitUnicodeString(&subValDword,L"TestCapValueDWORD");

                ULONG data = 0xaaaaaaaa;

                ntStatus = ZwSetValueKey(hCapabilityKeyHandle,&subValDword,0,REG_DWORD,&data,sizeof(ULONG));
                ZwClose(hCapabilityKeyHandle);
            }
        }
        ZwClose(hDeviceParametersKey);
        ExFreePool(pSymbolicNameList);
    }

    return ntStatus;
}
```
