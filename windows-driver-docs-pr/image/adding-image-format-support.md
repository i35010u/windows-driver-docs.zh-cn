---
title: 添加图像格式支持
description: 添加图像格式支持
ms.assetid: 1ffa7c0d-23ec-402a-a0b5-fb5596a851bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ef5bfb29959b7ae10378fcff5ab3ebbcc671373
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367106"
---
# <a name="adding-image-format-support"></a>添加图像格式支持





WIA 微型驱动程序报告给 WIA 服务中的图像格式[ **IWiaMiniDrv::drvGetWiaFormatInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff543986)方法。

### <a href="" id="implementing-iwiaminidrv-drvgetwiaformatinfo"></a>实现 IWiaMiniDrv::drvGetWiaFormatInfo

WIA 服务调用**IWiaMiniDrv::drvGetWiaFormatInfo**方法来获取的 WIA 设备支持 TYMED 和格式对。

WIA 驱动程序应分配内存 （以将存储在此 WIA 驱动程序，并释放此 WIA 驱动程序） 包含一个数组 WIA\_格式\_信息结构 （Microsoft Windows SDK 文档中所述）。 指向 WIA 驱动程序分配内存的指针应传递给*ppwfi*。 这不是直接，但使用指向指针的指针。 在以下示例中， *ppwfi* m 的地址设置\_WIAFormatInfo\[0\]，这反过来计算结果为地址结构的第一个成员。

请务必注意 WIA 服务不会释放此内存。 它负责 WIA 驱动程序来管理此分配的内存。

WIA 驱动程序应写入到的内存位置中分配的结构数*pcelt*参数所指向。

WIA 设备应设置**guidFormatID** WIA 的成员\_格式\_信息结构与图像格式的 GUID。 设备应设置**lTymed**图像格式的 GUID 与关联到 TYMED 值此结构的成员：

有效值 TYMED （也称为"媒体类型"） 为：

TYMED\_文件

TYMED\_多页\_文件

TYMED\_回调

TYMED\_多页\_回调

下面的示例演示的实现[ **IWiaMiniDrv::drvGetWiaFormatInfo**](https://msdn.microsoft.com/library/windows/hardware/ff543986):

```cpp
HRESULT _stdcall CWIADevice::drvGetWiaFormatInfo(
  BYTE            *pWiasContext,
  LONG            lFlags,
  LONG            *pcelt,
  WIA_FORMAT_INFO **ppwfi,
  LONG            *plDevErrVal)
{
    //
    // If the caller did not pass in the correct parameters,
    // then fail the call with E_INVALIDARG.
    //

    if ((!pWiasContext)||(!plDevErrVal)||(!pcelt)||(!ppwfi)) {
        return E_INVALIDARG;
    }

    //
    // check if WIA_FORMAT_INFO array has been initialized.
    //
    // NOTE: m_WIAFormatInfo is a member variable that has been
    //       defined as    WIA_FORMAT_INFO m_WIAFormatInfo[2];
    //
    //

    if (m_WIAFormatInfo[0].lTymed == TYMED_NULL) {

        //
        // add all supported formats and corresponding TYMED values
        // here
        //

        m_WIAFormatInfo[0].guidFormatID = WiaImgFmt_MEMORYBMP;
        m_WIAFormatInfo[0].lTymed       = TYMED_CALLBACK;

        m_WIAFormatInfo[1].guidFormatID = WiaImgFmt_BMP;
        m_WIAFormatInfo[1].lTymed       = TYMED_FILE;
    }

    *plDevErrVal = 0;
    *ppwfi = &m_WIAFormatInfo[0];
    *pcelt = 2; // number of formats in returned array

    return S_OK;
}
```

 

 




