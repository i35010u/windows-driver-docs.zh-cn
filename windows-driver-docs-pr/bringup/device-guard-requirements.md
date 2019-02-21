---
title: 保护多个实现
description: 描述的行为和 MemoryOverwriteRequestControlLock UEFI 变量，修订版 2 的使用情况。
ms.assetid: 94F42629-3B76-4EB1-A5FA-4FA13C932CED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2beead842d1b671b84de6eb0ea167d88534417e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520161"
---
# <a name="secure-mor-implementation"></a>保护多个实现


**摘要**

-   MorLock，修订版 2 的行为

**上次更新时间**

-   2018 年 1 月

**适用于**

-   Windows 10
-   Oem 和 BIOS 供应商想要支持 Windows 10 Credential Guard 功能。

**正式规范**

-   [UEFI 规范](https://go.microsoft.com/fwlink/p/?LinkId=717873)
-   [电脑客户端工作组平台重置攻击缓解规范，版本 1.0](https://go.microsoft.com/fwlink/p/?LinkId=717870)

**推荐的读物**

-   [博客文章：保护 BitLocker 免遭冷攻击 （和其他威胁的侵害）]( https://go.microsoft.com/fwlink/p/?LinkId=717871)
-   [白皮书：除了具有 UEFI TPM2 支持 BIOS 中 EDKII 的教程]( https://go.microsoft.com/fwlink/p/?LinkId=717872)
-   [使用 Credential Guard 保护派生的域凭据]( https://go.microsoft.com/fwlink/p/?LinkId=717899)

描述的行为和使用情况`MemoryOverwriteRequestControlLock`UEFI 变量，修订版 2。

若要防止高级的内存攻击，现有系统 BIOS 安全缓解**MemoryOverwriteRequestControl**已改进为支持锁定更有效地防止新的威胁。  威胁模型扩展以包含攻击者作为主机操作系统内核，因此 ACPI 和 UEFI 内核权限级别执行的运行时服务是不受信任。  与安全启动实现类似，MorLock 应实现由主机操作系统内核 （例如，系统管理模式、 TrustZone、 BMC，等） 不能被篡改的特权的固件执行上下文中。  接口基于 UEFI 变量服务，UEFI 规范版本 2.5 时，名为"变量服务"部分 7.2 中描述。

**请注意**  调用此缓解*MorLock*，必须在所有新系统上实现并不仅限于系统的受信任的平台模块。 修订版本 2 添加了新功能*解锁*，以缓解启动性能问题，尤其是在较大内存系统上的。

**请注意 2**  有关 ACPI \_DSM 控件方法用于设置 MOR 位状态 (中的第 6 节所述[PC 客户端工作组平台重置攻击缓解规范，版本 1.0](https://go.microsoft.com/fwlink/p/?LinkId=717870)):    
Microsoft 建议删除此\_DSM 现代 BIOS 实现方法。  但是，如果 BIOS 实现这\_DSM 方法，它必须遵守 MorLock 的状态。  如果锁定 MorLock，带或不带密钥，这\_DSM 方法时不能更改 MOR 和返回值 1 对应于"常规失败"。  定义没有 ACPI 的机制来解锁 MorLock 修订版本 2。  请注意，Windows 不直接调用此\_DSM 方法，因为 Windows 7，并认为它已被否决。  某些 BIOS*间接*调用此\_DSM 方法时 Windows 将调用 ACPI \_PTS 作为 MOR 自动检测的干净关闭的实现 (如的第 2.3 节中所述[PC 客户端工作组平台重置攻击缓解规范，版本 1.0](https://go.microsoft.com/fwlink/p/?LinkId=717870))。  此 ACPI \_MOR 自动检测的 PTS 实现是在不完善的安全，不应使用。

## <a name="memoryoverwriterequestcontrollock"></a>MemoryOverwriteRequestControlLock


包含改进的缓解措施的 BIOS 在早期启动过程中创建此 UEFI 变量：

**注册表：** `{BB983CCF-151D-40E1-A07B-4A17BE168292}`

**名称：** `MemoryOverwriteRequestControlLock`

**属性：** NV+BS+RT

**GetVariable**中的值*数据*参数：0x0 （解锁）;0x1 （如果没有密钥锁定）;0x2 （用密钥锁定）

**SetVariable**中的值*数据*参数：0x0 （解锁）;0x1 （锁定）

## <a name="locking-with-setvariable"></a>使用 SetVariable 锁定


应在每次启动初始化 BIOS`MemoryOverwriteRequestControlLock`到单字节值 0x00 (，该值指示*解锁*) 之前启动设备选择 (BDS) 阶段 (驱动程序\#\# \# \#SYSPREP\#\#\#\#，启动\#\#\#\#，\*恢复\*，...)。 有关`MemoryOverwriteRequestControlLock`(和`MemoryOverwriteRequestControl`)、 BIOS 应防止删除的变量和属性必须固定到 NV + B + RT。

时**SetVariable**有关`MemoryOverwriteRequestControlLock`通过传递有效的非零值中首次调用时*数据*，两者的访问模式`MemoryOverwriteRequestControlLock`和`MemoryOverwriteRequestControl`为只读，指示已更改它们会被锁定。

修订版本 1 实现仅接受单字节的 0x00 或 0x01 的`MemoryOverwriteRequestControlLock`。

此外，修订版 2 接受一个 8 字节值，表示共享机密密钥。 如果在中指定任何其他值**SetVariable**，调用将失败状态 EFI\_无效\_参数。 若要生成该密钥，请使用如受信任的平台模块或硬件随机数字生成器的高质量平均信息量源。

设置项之后, 的调用方和固件应保存此密钥的副本在受保护的机密性的位置，例如 SMRAM IA32/X 64 或受保护的存储为服务的处理器上。

## <a name="getting-the-system-state"></a>获取系统状态


在修订版本 2 中，当`MemoryOverwriteRequestControlLock`和`MemoryOverwriteRequestControl`变量将被锁定的调用**SetVariable** （对于这些变量） 进行第一次检查的已注册项使用常量算法。 如果这两个密钥存在，并且匹配，恢复到未锁定状态的变量转换。 此第一次尝试后，或者不注册任何密钥，将此变量设置的后续尝试失败并且 EFI\_访问\_拒绝来阻止暴力攻击。 在这种情况下，重新启动系统应解锁变量的唯一方法。

操作系统检测是否存在`MemoryOverwriteRequestControlLock`并通过调用其状态**GetVariable**。 然后，系统可以锁定的当前值`MemoryOverwriteRequestControl`通过设置`MemoryOverwriteRequestControlLock`值为 0x1。 或者，它可以指定一个项来启用将来解锁后安全地清除内存的机密数据。

调用**GetVariable**为`MemoryOverwriteRequestControlLock`返回 0x0、 0x1 或 0x2 以指示未锁定，锁定没有密钥，或锁定状态，且密钥状态。

**请注意**  设置`MemoryOverwriteRequestControlLock`不会提交闪烁 （只需更改内部锁状态）。 获取变量返回的内部状态并永远不会公开该密钥。 以下各图详细介绍预期的行为。

 

由操作系统的示例用法

```cpp
if (gSecretsInMemory) 
{
    char data = 0x11;
    SetVariable(MemoryOverwriteRequestControl, sizeof(data), &data);
}
 
// check presence
status = GetVariable(MemoryOverwriteRequestControlLock, &value);  
    
if (SUCCESS(status)) 
{
    // first attempt to lock and establish a key 
    // note both MOR and MorLock are locked if successful

    GetRNG(8, keyPtr);
    status = SetVariable(MemoryOverwriteRequestControlLock, 8, keyPtr); 

    if (status != EFI_SUCCESS) 
    {
        // fallback to revision 1 behavior
        char data = 0x01;
        status = SetVariable(MemoryOverwriteRequestControlLock, 1, &data); 
        if (status != EFI_SUCCESS) { // log error, warn user }
    }
} 
else 
{
    // warn user about potentially unsafe system
}

// put secrets in memory

// … time passes …

// remove secrets from memory, flush caches

SetVariable(MemoryOverwriteRequestControlLock, 8, keyPtr)
```

## <a name="morlock-implementation-flow"></a>MorLock 实现流


这些流程图显示您的实现的预期的行为：

### <a name="initialization"></a>初始化

![morlock 初始化](images/morlock.png)

### <a name="setvariable-flow"></a>SetVariable 流

![morlock 编程流](images/morlock1.png)

### <a name="unlocked-state-flow-for-setvariable"></a>SetVariable 的解除锁定的状态流

![解锁 morlock 流](images/morlock2.png)

### <a name="locked-state-flow-for-setvariable"></a>锁定 SetVariable 的状态流

![morlock 锁定流](images/morlock3.png)

### <a name="flow-for-getvariable"></a>GetVariable 的流

![morlock getvariable](images/morlock4.png)

## <a name="related-topics"></a>相关主题
[适用于 SoC 平台上的所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md#security-requirements)  
[电脑客户端工作组平台重置攻击缓解规范，版本 1.0](https://go.microsoft.com/fwlink/p/?LinkId=717870)  
[保护 BitLocker 免遭冷攻击 （和其他威胁的侵害）]( https://go.microsoft.com/fwlink/p/?LinkId=717871)  
[除了具有 UEFI TPM2 支持 BIOS 中 EDKII 的教程]( https://go.microsoft.com/fwlink/p/?LinkId=717872)  
[使用 Credential Guard 保护派生的域凭据]( https://go.microsoft.com/fwlink/p/?LinkId=717899)  
[UEFI 规范](https://go.microsoft.com/fwlink/p/?LinkId=717873)  



