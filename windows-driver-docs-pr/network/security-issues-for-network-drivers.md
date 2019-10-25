---
title: 网络驱动程序的安全问题
description: 本部分介绍特定于网络驱动程序的安全问题
ms.assetid: 04400213-9bd4-4dbe-b302-24917450829f
keywords:
- 网络驱动程序 WDK，安全性
- 安全 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9677778e08ad80f2315d47fe3889a489d9d8d646
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841991"
---
# <a name="security-issues-for-network-drivers"></a>网络驱动程序的安全问题

有关编写安全驱动程序的一般讨论，请参阅[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)。

除了遵循安全的编码实践和常规设备驱动程序指南之外，网络驱动程序还应执行以下操作以增强安全性：

- 所有网络驱动程序都应该验证它们从注册表中读取的值。 具体而言， [**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)或[**NdisReadNetworkAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress)的调用方不能对从注册表中读取的值作出任何假设，并且必须验证其所读取的每个注册表值。 如果**NdisReadConfiguration**的调用方确定某个值超出界限，则应改用默认值。 如果**NdisReadNetworkAddress**的调用方确定某个值超出界限，则应改为使用永久的媒体访问控制（MAC）地址或默认地址。

## <a name="oid-specific-issues"></a>OID 特定的问题

- 微型端口驱动程序（在其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)或[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数中）应验证请求设置的驱动程序的任何对象标识符（OID）值。 如果驱动程序确定要设置的值超出界限，则该设置请求应失败。 有关对象标识符的详细信息，请参阅[获取并设置微型端口驱动程序信息和对 WMI 的 NDIS 支持](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

- 如果中间驱动程序的*MiniportOidRequest*函数未将设置操作传递到基础微型端口驱动程序，则该函数应验证 OID 值。 有关详细信息，请参阅[中间驱动程序查询和设置操作](intermediate-driver-query-and-set-operations.md)。

### <a name="query-oid-security-guidelines"></a>查询 OID 安全准则

大多数查询 Oid 都可以由系统上的任何 usermode 应用程序发出。 遵循这些特定的查询 Oid 指导原则。

1. 始终验证缓冲区大小是否足以满足输出的大小。 任何没有输出缓冲区大小检查的查询 OID 处理程序都具有安全错误。

    ```c++
    if (oid->DATA.QUERY_INFORMATION.InformationBufferLength < sizeof(ULONG)) {
        oid->DATA.QUERY_INFORMATION.BytesNeeded = sizeof(ULONG);
        return NDIS_STATUS_INVALID_LENGTH;
    }
    ```

2. 始终向 BytesWritten 写入正确的最小值。 这是一个用于分配 `oid->BytesWritten = oid->InformationBufferLength` 的红色标志，如以下示例中所示。

    ```c++
    // ALWAYS WRONG
    oid->DATA.QUERY_INFORMATION.BytesWritten = DATA.QUERY_INFORMATION.InformationBufferLength; 
    ```

    操作系统会将 BytesWritten 字节复制回 usermode 应用程序。 如果 BytesWritten 大于驱动程序实际写入的字节数，则 OS 可能最终会将未初始化的内核内存复制回 usermode，这将是一个信息泄漏漏洞。 请改用类似于下面的代码：

    ```c++
    oid->DATA.QUERY_INFORMATION.BytesWritten = sizeof(ULONG);
    ``` 

3. 从不从缓冲区中读取值。 在某些情况下，OID 的输出缓冲区直接映射到恶意 usermode 进程。 恶意过程可以在写入输出缓冲区后更改输出缓冲区。 例如，以下代码可能会受到攻击，因为攻击者可以在写入后更改 NumElements：

    ```c++
    output->NumElements = 4;
    for (i = 0 ; i < output->NumElements ; i++) {
        output->Element[i] = . . .;
    }
    ```
    若要避免从缓冲区中读取，请保留本地副本。 例如，若要修复上述示例，请引入一个新的堆栈变量：

    ```c++
    ULONG num = 4;
    output->NumElements = num;
    for (i = 0 ; i < num; i++) {
        output->Element[i] = . . .;
    }
    ```

    利用此方法，for 循环从驱动程序的堆栈变量 `num` 而不是从其输出缓冲区中读取。 驱动程序还应将输出缓冲区标记 `volatile` 关键字，以防止编译器无提示地撤消此修补程序。

### <a name="set-oid-security-guidelines"></a>设置 OID 安全指导原则

大多数集 Oid 都可以由在管理员或系统安全组中运行的 usermode 应用程序发出。 尽管这些应用程序通常是受信任的应用程序，但微型端口驱动程序仍然不得允许内存损坏或内核代码注入。 对于设置 Oid，请遵循以下特定规则：

1.  始终验证输入是否足够大。 不带输入缓冲区大小检查的任何 OID 集处理程序都具有安全漏洞。

    ```c++
    if (oid->DATA.SET_INFORMATION.InformationBufferLength < sizeof(ULONG)) {
        return NDIS_STATUS_INVALID_LENGTH;
    }
    ```

2. 当验证具有嵌入偏移量的 OID 时，必须验证嵌入的缓冲区是否位于 OID 有效负载中。 这需要进行多项检查。 例如， [OID_PM_ADD_WOL_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)可能会提供需要检查的嵌入模式。 正确的验证需要检查：

    1. InformationBufferSize > = sizeof （NDIS_PM_PACKET_PATTERN）

        ```c++
        PmPattern = (PNDIS_PM_PACKET_PATTERN) InformationBuffer;
        if (InformationBufferLength < sizeof(NDIS_PM_PACKET_PATTERN))
        {
            Status = NDIS_STATUS_BUFFER_TOO_SHORT;
            *BytesNeeded = sizeof(NDIS_PM_PACKET_PATTERN);
            break;
        }
        ```

    2. 模式 > PatternOffset + 模式 > PatternSize 不溢出

        ```c++
        ULONG TotalSize = 0;
        if (!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternSize, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```

        可以使用类似于以下示例的代码来合并这两个检查：

        ```c++
        ULONG TotalSize = 0;
        if (InformationBufferLength < sizeof(NDIS_PM_PACKET_PATTERN) ||
            !NT_SUCCESS(RtlUlongAdd(Pattern->PatternSize, Pattern->PatternOffset, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```
   
    3. InformationBuffer + 模式 > PatternOffset + 模式-> PatternLength 未溢出

        ```c++
        ULONG TotalSize = 0;
        if (!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternLength, &TotalSize) ||
            (!NT_SUCCESS(RtlUlongAdd(TotalSize, InformationBuffer, &TotalSize) ||
            TotalSize > InformationBufferLength) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```

    4. 模式 > PatternOffset + 模式-> PatternLength < = InformationBufferSize

        ```c++
        ULONG TotalSize = 0;
        if(!NT_SUCCESS(RtlUlongAdd(Pattern->PatternOffset, Pattern->PatternLength, &TotalSize) ||
            TotalSize > InformationBufferLength)) 
        {
            return NDIS_STATUS_INVALID_LENGTH;
        }
        ```
   
### <a name="method-oid-security-guidelines"></a>方法 OID 安全指导原则

可以通过在管理员或系统安全组中运行的 usermode 应用程序来颁发方法 Oid。 它们是集和查询的组合，所以前面的指南列表还适用于方法 Oid。

## <a name="other-network-driver-security-issues"></a>其他网络驱动程序安全问题

- 许多 NDIS 微型端口驱动程序通过使用 NdisRegisterDeviceEx 来公开控制设备。 执行此操作的操作必须审核其 IOCTL 处理程序，并使用与 WDM 驱动程序相同的所有安全规则。 有关详细信息，请参阅[I/o 控制代码的安全问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/security-issues-for-i-o-control-codes)。

- 设计良好的 NDIS 微型端口驱动程序不应依赖于在特定的进程上下文中调用，也不应与 usermode 非常紧密交互（IOCTLs & Oid 就是例外）。 它将是一个红色标志，用于查看打开 usermode 句柄、执行 usermode 等待或分配的内存和 usermode 配额的小型端口。 应调查该代码。

- 大多数 NDIS 微型端口驱动程序不应涉及分析数据包有效负载。 但在某些情况下，可能需要这样做。 如果是这样，则应仔细审核此代码，因为驱动程序正在分析来自不受信任的源的数据。

- 与分配内核模式内存时的标准一样，NDIS 驱动程序应使用适当[的 NX 池选择机制](https://docs.microsoft.com/windows-hardware/drivers/kernel/nx-pool-opt-in-mechanisms)。 在 WDK 8 及更高版本中，已正确选择了 `NdisAllocate*` 系列的函数。

