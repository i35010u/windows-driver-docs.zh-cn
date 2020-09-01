---
title: 使用注册表项对象的句柄
description: 使用注册表项对象的句柄
ms.assetid: 25982249-31dc-4542-9ebb-139991619b40
keywords:
- 注册表-密钥对象 WDK 内核的句柄
- 注册表 WDK 内核，对象例程
- 驱动程序注册表信息 WDK 内核，对象例程
- 对象例程 WDK 内核
- 注册表-密钥对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15c325dcbe244b01df8ea6f213fbcfd6f5c3eb60
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187726"
---
# <a name="using-a-handle-to-a-registry-key-object"></a>使用注册表项对象的句柄





下表列出了驱动程序可以对开放密钥执行的操作，以及要调用的相应例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>要调用的例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>检查注册表项的属性，例如其名称或其子项的数目。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey" data-raw-source="[&lt;strong&gt;ZwQueryKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey)"><strong>ZwQueryKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>遍历密钥的子项，检查每个子项的属性。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey" data-raw-source="[&lt;strong&gt;ZwEnumerateKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)"><strong>ZwEnumerateKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>检查键值的属性，包括值的数据。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey" data-raw-source="[&lt;strong&gt;ZwQueryValueKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)"><strong>ZwQueryValueKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>遍历键的值，检查每个值的属性。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey" data-raw-source="[&lt;strong&gt;ZwEnumerateValueKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey)"><strong>ZwEnumerateValueKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>设置与某个键相关联的值的数据。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey" data-raw-source="[&lt;strong&gt;ZwSetValueKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)"><strong>ZwSetValueKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>删除密钥。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)"><strong>ZwDeleteKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>删除键值。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletevaluekey" data-raw-source="[&lt;strong&gt;ZwDeleteValueKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletevaluekey)"><strong>ZwDeleteValueKey</strong></a></p></td>
</tr>
</tbody>
</table>

 

一旦驱动程序完成其操作，它就必须调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 来关闭句柄，即使它已调用 **ZwDeleteKey** 来删除密钥。  (一旦某个密钥被删除，该密钥的所有打开句柄都将变为无效，但驱动程序仍须关闭该句柄。 ) 

下面的代码示例演示了如何为名为** \\ 注册表 \\ 计算机 \\ Software \\ **<em>MyCompany</em>MyApp 的密钥打开句柄 \\ *MyApp*，然后检索密钥数据并关闭句柄。

```cpp
//
// Get the frame location from the registry key
// HKLM\SOFTWARE\MyCompany\MyApp.
// For example: "FrameLocation"="X:\\MyApp\\Frames"
// 
HANDLE              handleRegKey = NULL;
for (int n = 0; n < 1; n++) 
{
    NTSTATUS           status = NULL;
    UNICODE_STRING     RegistryKeyName;
    OBJECT_ATTRIBUTES  ObjectAttributes;

    RtlInitUnicodeString(&RegistryKeyName, L"\\Registry\\Machine\\Software\\MyCompany\\MyApp");
    InitializeObjectAttributes(&ObjectAttributes, 
                               &RegistryKeyName,
                               OBJ_CASE_INSENSITIVE | OBJ_KERNEL_HANDLE,
                               NULL,    // handle
                               NULL);
    status = ZwOpenKey(&handleRegKey, KEY_READ, &ObjectAttributes);

    // If the driver cannot open the key, the driver cannot continue. 
    // In this situation, the driver was probably set up incorrectly 
    // and worst case, the driver cannot stream.
    if( NT_SUCCESS(status) == FALSE ) 
    {
        break;
    }
    // The driver obtained the registry key.
    PKEY_VALUE_FULL_INFORMATION  pKeyInfo = NULL;
    UNICODE_STRING               ValueName;
    ULONG                        ulKeyInfoSize = 0;
    ULONG                        ulKeyInfoSizeNeeded = 0;

    // The driver requires the following value.
    RtlInitUnicodeString(&ValueName, L"FrameLocation");

    // Determine the required size of keyInfo.
    status = ZwQueryValueKey( handleRegKey,
                              &ValueName,
                              KeyValueFullInformation,
                              pKeyInfo,
                              ulKeyInfoSize,
                              &ulKeyInfoSizeNeeded );

    // The driver expects one of the following errors.
    if( (status == STATUS_BUFFER_TOO_SMALL) || (status == STATUS_BUFFER_OVERFLOW) )
    {
        // Allocate the memory required for the key.
        ulKeyInfoSize = ulKeyInfoSizeNeeded;
        pKeyInfo = (PKEY_VALUE_FULL_INFORMATION) ExAllocatePoolWithTag( NonPagedPool, ulKeyInfoSizeNeeded, g_ulTag);
        if( NULL == pKeyInfo )
        {
            break;
        }
        RtlZeroMemory( pKeyInfo, ulKeyInfoSize );

        // Get the key data.
        status = ZwQueryValueKey( handleRegKey,
                                  &ValueName,
                                  KeyValueFullInformation,
                                  pKeyInfo,
                                  ulKeyInfoSize,
                                  &ulKeyInfoSizeNeeded );
        if( (status != STATUS_SUCCESS) || (ulKeyInfoSizeNeeded != ulKeyInfoSize) || (NULL == pKeyInfo) )
        {
            break;
        }

        // Fill in the frame location if it has not been filled in already.
        if ( NULL == m_szwFramePath )
        {
            m_ulFramePathLength = pKeyInfo->DataLength;
            ULONG_PTR   pSrc = NULL;

            pSrc = (ULONG_PTR) ( (PBYTE) pKeyInfo + pKeyInfo->DataOffset);

            m_szwFramePath = (LPWSTR) ExAllocatePoolWithTag( NonPagedPool, m_ulFramePathLength, g_ulTag);
            if ( NULL == m_szwFramePath )
            {
                m_ulFramePathLength = 0;
                break;
            }

            // Copy the frame path.
            RtlCopyMemory(m_szwFramePath, (PVOID) pSrc, m_ulFramePathLength);
        }
        // The driver is done with the pKeyInfo.
        xFreePoolWithTag(pKeyInfo, g_ulTag);

    } // if( (status == STATUS_BUFFER_TOO_SMALL) || (status == STATUS_BUFFER_OVERFLOW) )
} // Get the Frame location from the registry key.

// All done with the registry.
if (NULL != handleRegKey)
{
    ZwClose(handleRegKey);
}
```

系统会将密钥更改缓存在内存中，并每隔几秒将它们写入磁盘。 若要强制更改磁盘的密钥，请调用 [**ZwFlushKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey)。

若要通过更简单的接口操作注册表，驱动程序还可以调用 **Rtl*Xxx*registry * Xxx*** 例程。 有关详细信息，请参阅 [注册表运行时库例程](registry-run-time-library-routines.md)。

 

