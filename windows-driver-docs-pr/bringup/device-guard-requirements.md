---
title: 安全 MOR 实现
description: 描述 MemoryOverwriteRequestControlLock UEFI 变量的行为和用法，版本2。
ms.assetid: 94F42629-3B76-4EB1-A5FA-4FA13C932CED
ms.date: 01/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 67296395acd0e9a83c2c5dd71b3459854fd59ce1
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769397"
---
# <a name="secure-mor-implementation"></a>安全 MOR 实现

## <a name="summary"></a>摘要

- MorLock，修订版2的行为

## <a name="last-updated"></a>上次更新时间

- 2018 年 1 月

## <a name="applies-to"></a>适用于

- Windows 10

- 要支持 Windows 10 的 Credential Guard 功能的 Oem 和 BIOS 供应商。

## <a name="official-specifications"></a>官方规范

- [UEFI 规范](https://uefi.org/specifications)

- [电脑客户端工作组平台重置攻击缓解规范，版本1.0 （PDF 下载）](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)

## <a name="recommended-reading"></a>推荐阅读内容

- [博客文章：保护 BitLocker 免受冷攻击（和其他威胁）](https://docs.microsoft.com/archive/blogs/si_team/protecting-bitlocker-from-cold-attacks-and-other-threats)

- [白皮书：在 EDKII 中使用 UEFI TPM2 支持的 BIOS 教程](https://github.com/tianocore/edk2-platforms/blob/devel-MinPlatform/Platform/Intel/MinPlatformPkg/Docs/A_Tour_Beyond_BIOS_Open_Source_IA_Firmware_Platform_Design_Guide_in_EFI_Developer_Kit_II%20-%20V2.pdf)

- [使用 Credential Guard 保护派生的域凭据](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard)

## <a name="overview"></a>概述

本主题介绍 UEFI 变量的行为和用法 `MemoryOverwriteRequestControlLock` ，版本2。

为了防止高级内存攻击，将改进现有的系统 BIOS 安全缓解**MemoryOverwriteRequestControl** ，以支持锁定以应对新的威胁。  威胁模型已扩展为包括主机操作系统内核作为攻击者，因此，在内核权限级别执行的 ACPI 和 UEFI 运行时服务不受信任。  与安全启动实现类似，MorLock 应在特权固件执行上下文中实现，主机操作系统内核无法篡改该上下文（例如，系统管理模式、TrustZone、BMC，等等）。  接口是基于 UEFI 变量服务构建的，UEFI 规范版本2.5 中的 "变量服务" 一7.2 节中介绍了该服务。

此缓解措施称为*MorLock*，必须在所有新系统上实现，而不仅限于具有受信任的平台模块的系统。 修订版2添加了新功能 "*解锁*"，以减轻启动性能问题，尤其是在大型内存系统上。

有关 \_ 用于设置 MOR 位状态的 ACPI DSM 控制方法（如[电脑客户端工作组平台重置攻击缓解规范的第6节中所述，版本1.0 （PDF 下载））](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)，建议 \_ 从新式 BIOS 实现中删除此 DSM 方法。  但是，如果 BIOS 实现了此 \_ DSM 方法，则它必须遵循 MorLock 的状态。  如果 MorLock 已锁定，无论是否有密钥，此 \_ DSM 方法都必须无法更改 MOR，并返回对应于 "常规失败" 的值1。  未定义 ACPI 机制来解锁 MorLock 版本2。  

请注意，Windows 不会直接调用此 \_ DSM 方法，因为 windows 7 会将其视为已弃用。  某些 BIOS *indirectly* \_ 在 Windows 调用 ACPI \_ Pt 作为 MOR 自动检测干净关闭的实现时，间接调用此 DSM 方法（如[PC 客户端工作组平台重置攻击缓解1.0 规范的2.3 节（PDF 下载）](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)中所述）。  

\_MOR 自动检测的这一 ACPI 实现是安全缺少的，不应使用。

## <a name="memoryoverwriterequestcontrollock"></a>MemoryOverwriteRequestControlLock

包含改进的缓解措施的 BIOS 将在早期启动过程中创建此 UEFI 变量：

**VendorGuid：**`{BB983CCF-151D-40E1-A07B-4A17BE168292}`

**名称：**`MemoryOverwriteRequestControlLock`

**属性：** NV + BS.1770 + RT

*数据*参数中的**GetVariable**值：0x0 （未锁定）;0x1 （已锁定但没有密钥）;0x2 （已锁定并带有密钥）

*数据*参数中的**SetVariable**值：0x0 （未锁定）;0x1 （锁定）

## <a name="locking-with-setvariable"></a>用 SetVariable 锁定

在每次启动时，在 `MemoryOverwriteRequestControlLock` 启动设备选择（BDS）阶段（驱动程序*unlocked* \# \# \# \# 、SYSPREP \# \# \# \# 、启动 \# \# \# \# 、 \* 恢复 \* 、...）之前，BIOS 应初始化为单字节值0x00 （表示未锁定）。 对于 `MemoryOverwriteRequestControlLock` （和 `MemoryOverwriteRequestControl` ），BIOS 应禁止删除变量，并且必须将属性固定到 NV + BS.1770 + RT。

当**SetVariable** `MemoryOverwriteRequestControlLock` 第一次调用 SetVariable 时，如果在*数据*中传递有效的非零值，则和的访问模式 `MemoryOverwriteRequestControlLock` `MemoryOverwriteRequestControl` 将更改为只读，指示它们已锁定。

修订版1实现仅接受的单个字节为0x00 或 0x01 `MemoryOverwriteRequestControlLock` 。

修订版本2还接受表示共享机密密钥的8字节值。 如果在**SetVariable**中指定了其他任何值，则调用失败，状态为 "EFI \_ 无效 \_ 参数"。 若要生成该密钥，请使用高质量熵源，例如受信任的平台模块或硬件随机数生成器。

设置密钥后，调用方和固件应将此密钥的副本保存在一个机密性保护的位置，例如 IA32/X64 上的 SMRAM 或具有受保护存储的服务处理器。

## <a name="getting-the-system-state"></a>获取系统状态

在修订版2中，当 `MemoryOverwriteRequestControlLock` 和 `MemoryOverwriteRequestControl` 变量锁定时，将首先使用固定时间算法对照注册的密钥来检查**SetVariable**的调用（对于这些变量）。 如果两个键都存在并且匹配，则变量将转换回未锁定状态。 在第一次尝试或未注册任何密钥后，尝试设置此变量的后续尝试将失败，并 \_ 拒绝 EFI 访问， \_ 以防止强力攻击。 在这种情况下，系统重新启动应该是解锁变量的唯一方法。

操作系统 `MemoryOverwriteRequestControlLock` 通过调用**GetVariable**检测是否存在及其状态。 然后，系统可以 `MemoryOverwriteRequestControl` 通过将值设置为0x1 来锁定的当前值 `MemoryOverwriteRequestControlLock` 。 另外，它还可以指定一个密钥，以便在将来安全地从内存中清除机密数据后，启用解锁。

调用**GetVariable**以 `MemoryOverwriteRequestControlLock` 返回0x0、0x1 或0x2，以指示未锁定、已锁定但没有密钥，或锁定为密钥状态。

设置不 `MemoryOverwriteRequestControlLock` 会提交到 flash （只更改内部锁定状态）。 获取该变量将返回内部状态，并且永远不会公开该密钥。

操作系统使用情况示例：

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

SetVariable(MemoryOverwriteRequestControlLock, 8, keyPtr);
```

## <a name="morlock-implementation-flow"></a>MorLock 实现流

以下流程图显示了实现的预期行为：

### <a name="initialization"></a>初始化

![morlock 初始化](images/morlock.png)

### <a name="setvariable-flow"></a>SetVariable flow

![morlock 编程流](images/morlock1.png)

### <a name="unlocked-state-flow-for-setvariable"></a>SetVariable 的未锁定状态流

![morlock 解除锁定的流](images/morlock2.png)

### <a name="locked-state-flow-for-setvariable"></a>SetVariable 的锁定状态流

![morlock 锁定的流](images/morlock3.png)

### <a name="flow-for-getvariable"></a>GetVariable 的流

![morlock getvariable](images/morlock4.png)

## <a name="see-also"></a>另请参阅

[适用于 SoC 平台上的所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md#security-requirements)

[电脑客户端工作组平台重置攻击缓解规范，版本1.0 （PDF 下载）](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)  

[保护 BitLocker 免受冷攻击（和其他威胁）](https://docs.microsoft.com/archive/blogs/si_team/protecting-bitlocker-from-cold-attacks-and-other-threats)  

[在 EDKII 中使用 UEFI TPM2 支持的 BIOS 之外的教程](https://github.com/tianocore/edk2-platforms/blob/devel-MinPlatform/Platform/Intel/MinPlatformPkg/Docs/A_Tour_Beyond_BIOS_Open_Source_IA_Firmware_Platform_Design_Guide_in_EFI_Developer_Kit_II%20-%20V2.pdf)

[使用 Credential Guard 保护派生的域凭据](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard)

[UEFI 规范](https://uefi.org/specifications)  
