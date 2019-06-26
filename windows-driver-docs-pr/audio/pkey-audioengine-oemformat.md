---
title: PKEY\_AudioEngine\_OEMFormat
description: PKEY\_AudioEngine\_OEMFormat
ms.assetid: a1587f46-1c21-4419-a1a4-81fe299c6871
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c4299536514cc9ac11f244cae8b45a2e940eb11
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355291"
---
# <a name="pkeyaudioengineoemformat"></a>PKEY\_AudioEngine\_OEMFormat


在 Windows Vista 及更高版本，**主键\_AudioEngine\_OEMFormat**属性键标识的音频端点设备的默认流格式。 呈现和捕获设备具有默认格式。 全局音频引擎使用设备的默认格式连接到共享模式下操作设备。 安装设备的 INF 文件加载到注册表中设备的默认格式。 用户可以更改通过 Windows 多媒体控制面板 (Mmsys.cpl) 的默认格式。 Windows XP 和早期版本的 Windows 不支持**主键\_AudioEngine\_OEMFormat**属性键。

INF 文件在该设备的添加注册表部分中指定音频端点设备的默认格式。 下面的 INF 示例演示将终结点设备的默认格式加载到注册表添加注册表部分。

```inf
;;
;; Identify endpoint device as a set of speakers.
;; Set default format to 48-kHz, 16-bit stereo.
;; Add endpoint extension property page.
;;
[OEMSettingsOverride.AddReg]
HKR,"EP\\0", %PKEY_AudioEndpoint_Association%,,%KSNODETYPE_SPEAKER%
HKR,"EP\\0", %PKEY_AudioEngine_OEMFormat%, %REG_BINARY%, 41,00,00,00,28,00,00,00,
 FE,FF,02,00,80,BB,00,00,00,EE,02,00,04,00,10,00,16,00,10,00,03,00,00,00,01,00,
 00,00,00,00,10,00,80,00,00,AA,00,38,9B,71
HKR,"EP\\0", %PKEY_AudioEndpoint_ControlPanelProvider%,,%AUDIOENDPOINT_EXT_UI_CLSID
```

前面的示例摘自 Sysfx 音频示例位于 Windows 驱动程序工具包中的文件 Sysfx.inf。 此 INF 文件的字符串部分包含以下定义。

```inf
PKEY_AudioEndpoint_ControlPanelProvider = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},1"
PKEY_AudioEndpoint_Association          = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioEngine_OEMFormat              = "{E4870E26-3CC5-4CD2-BA46-CA0A9A70ED04},3"
```

在上述示例中，添加注册表部分 OEMSettingsOverride.AddReg 的名称定义由[ **AddReg** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)指令 Sysfx.inf 界面安装部分中。 前面的示例中添加终结点号 0 的多个属性 (由字符串"EP\\\\0") 到设备接口的注册表项。 (如果设备接口表示[批筛选器](https://docs.microsoft.com/windows-hardware/drivers/audio/wave-filters)与多个终结点，额外的终结点是编号 1，2，依此类推。)有关接口安装部分的详细信息，请参阅[ **INF AddInterface 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)。

应用程序的 INF 文件已创建三个属性键和相关联的值加载到注册表后，可以通过获取访问属性[IPropertyStore](https://docs.microsoft.com/windows/desktop/api/propsys/nn-propsys-ipropertystore)终结点设备的接口。 标头文件 Mmdeviceapi.h Windows SDK 中包含 C /C++的三个属性键定义。 有关获取 IPropertyStore 接口的详细信息，请参阅的说明[ **IMMDevice::OpenPropertyStore** ](https://docs.microsoft.com/windows/desktop/api/mmdeviceapi/nf-mmdeviceapi-immdevice-openpropertystore) Windows SDK 文档中的方法。

在前面的示例 INF 中，**主键\_AudioEndpoint\_关联**属性键标识终结点设备 KS pin 类别的 GUID。 **主键\_AudioEndpoint\_ControlPanelProvider**属性键标识的 COM 接口对象，用于提供到 Mmsys.cpl 中的终结点的属性页的属性值的类 GUID设备。 有关这些属性密钥的详细信息，请参阅 Windows SDK 文档。 详细了解 KS 固定类别 Guid，请参阅[Pin Category 属性](https://docs.microsoft.com/windows-hardware/drivers/audio/pin-category-property)。

在前面的示例 INF 中，属性值与该键相关联**主键\_AudioEngine\_OEMFormat**属性键是 48 字节 REG\_二进制值，该值包含一个序列化表示形式[ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)或[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)描述格式的结构。 若要计算 REG\_要与关联的二进制数据值**主键\_AudioEngine\_OEMFormat**属性键、 嵌入**WAVEFORMATEX**或**WAVEFORMATEXTENSIBLE**结构中**PropVariant**结构，并序列化**PropVariant**结构通过调用**StgSerializePropVariant**函数。 有关详细信息**PropVariant**结构并**StgSerializePropVariant**函数中，请参阅 Windows SDK 文档。

下面的代码示例是一个控制台应用程序打印 REG\_INF 上例中所显示的二进制数据。

```cpp
//
// Embed a WAVEFORMATEXTENSIBLE structure in a PropVariant
// container, and print the PropVariant structure as a
// serialized stream of bytes in REG_BINARY format.
//

#include <stdio.h>
#include <wtypes.h>
#include <propidl.h>
#include <propvarutil.h>
#include <mmreg.h>
#include <ks.h>
#include <ksmedia.h>

void PrintSerializedFormat(WAVEFORMATEX *pWfx)
{
    HRESULT hr;
    PROPVARIANT var;
    SERIALIZEDPROPERTYVALUE* pVal;
    ULONG cb;

    // Create a VT_BLOB from the WAVEFORMATEX structure.
    var.vt = VT_BLOB;
    var.blob.cbSize = sizeof(*pWfx) + pWfx->cbSize;
    var.blob.pBlobData = (BYTE*)pWfx;

    // Serialize the PROPVARIANT structure. The serialized byte stream
    // will eventually be written to the registry as REG_BINARY data.
    hr = StgSerializePropVariant(&var, &pVal, &cb);
    if (SUCCEEDED(hr))
    {
        // Write the binary data to stdout. Format the output so you can
        // copy and paste it directly into the INF file as REG_BINARY data.
        for (UINT i = 0; i < cb; i++)
        {
            BYTE b = ((BYTE*)pVal)[i];
            wprintf(L"%2.2X,", b);
        }

        wprintf(L"\n");
        CoTaskMemFree(pVal);
    }
}

//
// Use a WAVEFORMATEXTENSIBLE structure to specify the format
// for a 48-kHz, 16-bit, (2-channel) stereo audio stream.
//
void main()
{
    WAVEFORMATEXTENSIBLE wfx;

    wfx.Format.wFormatTag = WAVE_FORMAT_EXTENSIBLE;
    wfx.Format.nChannels = 2;
    wfx.Format.nSamplesPerSec = 48000;
    wfx.Format.nAvgBytesPerSec = 4*48000;
    wfx.Format.nBlockAlign = 4;
    wfx.Format.wBitsPerSample = 16;
    wfx.Format.cbSize = sizeof(WAVEFORMATEXTENSIBLE) - sizeof(WAVEFORMATEX);
    wfx.Samples.wValidBitsPerSample = 16;
    wfx.dwChannelMask = 3;
    wfx.SubFormat = KSDATAFORMAT_SUBTYPE_PCM;

    PrintSerializedFormat(&wfx.Format);
}
```

在前面的代码示例的主函数创建[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)结构来描述的默认格式。 您可以修改主函数以创建[ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)或**WAVEFORMATEXTENSIBLE**结构来描述终结点设备的默认格式。

在前面的代码示例 PrintSerializedFormat 函数序列化格式描述和打印 REG 形式的序列化的格式说明\_二进制数据。 可以复制函数生成的打印的输出并将其粘贴到您的 INF 文件。

 

 





