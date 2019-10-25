---
title: PKEY\_AudioEngine\_OEMFormat
description: PKEY\_AudioEngine\_OEMFormat
ms.assetid: a1587f46-1c21-4419-a1a4-81fe299c6871
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d20c3384d555edb36f7274663beb2e3cd1e3a8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832489"
---
# <a name="pkey_audioengine_oemformat"></a>PKEY\_AudioEngine\_OEMFormat


在 Windows Vista 和更高版本中， **PKEY\_AudioEngine\_OEMFormat**属性键标识音频终结点设备的默认流格式。 呈现和捕获设备都具有默认格式。 全局音频引擎使用设备的默认格式连接到设备以进行共享模式操作。 安装设备的 INF 文件会将设备的默认格式加载到注册表中。 用户可以通过 Windows 多媒体控制面板（Mmsys）更改默认格式。 Windows XP 和早期版本的 Windows 不支持**PKEY\_AudioEngine\_OEMFormat**属性键。

INF 文件在该设备的 "外接程序" 部分中指定音频终结点设备的默认格式。 以下 INF 示例显示了一个将终结点设备的默认格式加载到注册表中的 "添加注册表" 部分。

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

前面的示例取自 Windows 驱动程序工具包中的 Sysfx 音频示例中的文件 Sysfx。 此 INF 文件的字符串部分包含以下定义。

```inf
PKEY_AudioEndpoint_ControlPanelProvider = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},1"
PKEY_AudioEndpoint_Association          = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioEngine_OEMFormat              = "{E4870E26-3CC5-4CD2-BA46-CA0A9A70ED04},3"
```

在前面的示例中，add-registry 部分的名称 OEMSettingsOverride AddReg，它是由 Sysfx 中接口安装部分的[**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)指令定义的。 前面的示例将终结点编号0（由字符串 "EP\\\\0" 标识）的多个属性添加到设备接口的注册表项。 （如果设备接口表示具有多个终结点的[波形筛选器](https://docs.microsoft.com/windows-hardware/drivers/audio/wave-filters)，则附加终结点的编号为1、2，依此类推。）有关接口安装部分的详细信息，请参阅[**INF AddInterface 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)。

在 INF 文件创建了三个属性键并将其关联值加载到注册表中后，应用程序可以通过获取终结点设备的[IPropertyStore](https://docs.microsoft.com/windows/desktop/api/propsys/nn-propsys-ipropertystore)接口访问这些属性。 Windows SDK 中的头文件 Mmdeviceapi 包含三个属性键C++的 C/定义。 有关获取 IPropertyStore 接口的详细信息，请参阅 Windows SDK 文档中的[**IMMDevice：： OpenPropertyStore**](https://docs.microsoft.com/windows/desktop/api/mmdeviceapi/nf-mmdeviceapi-immdevice-openpropertystore)方法说明。

在上述 INF 示例中， **PKEY\_AudioEndpoint\_Association**属性键用于标识终结点设备的 KS PIN 类别 GUID。 **PKEY\_AudioEndpoint\_ControlPanelProvider**属性键标识 COM 接口对象的类 GUID，该对象向终结点设备的 Mmsys 中的属性页提供属性值。 有关这些属性键的详细信息，请参阅 Windows SDK 文档。 有关 KS pin 类别 Guid 的详细信息，请参阅[固定类别属性](https://docs.microsoft.com/windows-hardware/drivers/audio/pin-category-property)。

在前面的 INF 示例中，与**PKEY\_AudioEngine\_OEMFormat**属性键关联的属性值是一个48字节的 REG\_二进制值，它包含[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)的序列化表示形式，或描述格式的[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构。 若要计算 REG\_要与**PKEY\_AudioEngine\_OEMFormat**属性键关联的二进制数据值，请在**WAVEFORMATEXTENSIBLE**结构中嵌入**WAVEFORMATEX**或**PropVariant**结构，并通过调用**StgSerializePropVariant**函数序列化**PropVariant**结构。 有关**PropVariant**结构和**StgSerializePropVariant**函数的详细信息，请参阅 Windows SDK 文档。

下面的代码示例是一个控制台应用程序，该应用程序打印上一 INF 示例中显示的 REG\_二进制数据。

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

前面的代码示例中的 main 函数创建一个[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构来说明默认格式。 您可以修改 main 函数以创建[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)或**WAVEFORMATEXTENSIBLE**结构来描述终结点设备的默认格式。

前面的代码示例中的 PrintSerializedFormat 函数序列化格式说明，并将序列化格式说明打印为 REG\_二进制数据。 可以复制该函数生成的打印输出，并将其粘贴到 INF 文件中。

 

 





