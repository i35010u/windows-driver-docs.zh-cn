---
title: 为数据分配内存
description: 为数据分配内存
ms.assetid: 15df5616-ddce-44ec-bd10-65cae0d95cf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5179716df822729294bf7c35291eb63b3bd89fcc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367079"
---
# <a name="allocating-memory-for-data"></a>为数据分配内存





WIA 服务依赖于中提供的信息[ **MINIDRV\_传输\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff545250)结构，以执行正确的数据传输。 此结构与 WIA 微型驱动程序相关的成员包括：

**bClassDrvAllocBuf** − WIA 服务分配一个布尔值。

**pTransferBuffer** − 指向内存的内存分配给传输的数据。

**lBufferSize** − 内存的大小由指向**pTransferBuffer**成员。

如果**bClassDrvAllocBuf** MINIDRV 成员\_传输\_上下文结构设置为**TRUE**，然后 WIA 服务为微型驱动程序分配内存。 如果**bClassDrvAllocBuf**成员设置为**FALSE**，WIA 服务未分配任何内存的微型驱动程序。

微型驱动程序应使用的内存分配**CoTaskMemAlloc**函数 （Microsoft Windows SDK 文档中所述）。 微型驱动程序然后应存储中的内存位置的指针**pTransferBuffer**和中的内存大小**lBufferSize** （以字节为单位）。

**BClassDrvAllocBuff**成员设置为**FALSE**才[ **WIA\_IPA\_TYMED** ](https://msdn.microsoft.com/library/windows/hardware/ff551656)属性设置为 TYMED\_文件或 TYMED\_多页\_文件，和[ **WIA\_IPA\_项\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551594)属性设置为零。

微型驱动程序必须小心以免 overfill 通过指向的缓冲区**pTransferBuffer**成员。 您可以避免这种情况中的写入数据量小于或等于中存储的值**lBufferSize**成员。

### <a name="enhancing-data-transfer-performance-by-using-minimum-buffer-size"></a>通过使用最小缓冲区大小的增强的数据传输性能

WIA 微型驱动程序可以控制设置在数据传输过程中使用的内存量[ **WIA\_IPA\_项\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551594)和[ **WIA\_IPA\_缓冲区\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551527)属性。

WIA 应用程序使用 WIA\_IPA\_缓冲区\_大小属性确定要在内存传输期间请求的最小传输缓冲区大小。 此值越大，请求的外就越大。 如果 WIA 应用程序请求的缓冲区，则在 WIA 值大小小于\_IPA\_缓冲区\_大小属性 WIA 服务将忽略此请求的大小和要求 WIA 微型驱动程序提供的缓冲区，则 WIA\_IPA\_缓冲区\_大小字节的大小。 WIA 服务始终要求提供 WIA 微型驱动程序至少缓冲区 WIA\_IPA\_缓冲区\_大小字节的大小。

**请注意**  值的 WIA\_IPA\_缓冲区\_大小属性包含为最小的应用程序可以请求在任何给定时间的数据量。 缓冲区大小越大，设备将较大的请求。 缓冲区大小太小可能会降低数据传输的性能。

 

建议设置 WIA\_IPA\_缓冲区\_大小属性设置为合理的大小，以允许设备将传输数据以高效的速率。 为此，为了确保获得最佳性能平衡请求 （缓冲区大小不太小） 数和需花时间请求 （缓冲区太大） 为你的设备数。

应设置[ **WIA\_IPA\_项\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551594)属性设置为零，如果 WIA 微型驱动程序可将数据传输。 如果传输类型为 TYMED\_文件或 TYMED\_多页\_文件时，它是为要传递给 WIA 服务函数写入文件的数据缓冲区分配内存的微型驱动程序的责任。 这提供了在实现中的一致性[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)方法。

[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)打算将数据从设备传输到应用程序时，由 WIA 服务调用的方法。 WIA 驱动程序应确定哪种类型的传输 （通过 WIA 服务） 应用程序正在请求，通过阅读**tymed**的成员[ **MINIDRV\_传输\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff545250):

**Tymed**成员，该应用程序设置，可以具有以下四个值之一：

<a href="" id="tymed-file"></a>TYMED\_文件  
数据传输到一个文件。

<a href="" id="tymed-multipage-file"></a>TYMED\_多页\_文件  
数据传输到多页的文件格式。

<a href="" id="tymed-callback"></a>TYMED\_回调  
将数据传输到内存中。

<a href="" id="tymed-multipage-callback"></a>TYMED\_多页\_回调  
将多个页的数据传输到内存。

不同 TYMED 设置 XXX\_回调，XXX\_文件更改调用应用程序的回调接口的使用情况。

### <a href="" id="tymed-callback-and-tymed-multipage-callback"></a>TYMED\_回调和 TYMED\_多页\_回调

有关内存传输问题[ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)回调：

(*pmdtc-&gt;pIWiaMiniDrvCallBack-&gt;MiniDrvCallback*下面的示例源代码中)

请使用以下值的回调：

<a href="" id="it-msg-data"></a>IT\_MSG\_DATA  
该驱动程序在传输数据。

<a href="" id="it-status-transfer-to-client"></a>IT\_状态\_传输\_TO\_客户端  
数据传输消息。

<a href="" id="lpercentcomplete"></a>*lPercentComplete*  
传输已完成的百分比。

<a href="" id="pmdtc--cboffset"></a>*pmdtc-&gt;cbOffset*  
更新到当前应用程序应在其中编写下一个数据块的位置。

<a href="" id="lbytesreceived"></a>*lBytesReceived*  
发送到应用程序的数据块区中的字节数。

<a href="" id="pmdtc"></a>*pmdtc*  
指向[ **MINIDRV\_传输\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff545250)结构，其中包含的数据传输值。

### <a href="" id="tymed-file-and-tymed-multipage-file"></a>TYMED\_文件和 TYMED\_多页\_文件

有关文件传输问题[ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)回调::

(*pmdtc-&gt;pIWiaMiniDrvCallBack-&gt;MiniDrvCallback*下面的示例源代码中)

请使用以下值的回调。

<a href="" id="it-msg-status"></a>IT\_MSG\_状态  
该驱动程序正在发送仅状态 （无数据）。

<a href="" id="it-status-transfer-to-client"></a>IT\_状态\_传输\_TO\_客户端  
数据传输消息。

<a href="" id="lpercentcomplete"></a>*lPercentComplete*  
传输已完成的百分比。

如果**ItemSize** MINIDRV 成员\_传输\_上下文结构设置为零，这表示对应用程序 WIA 驱动程序不知道所生成的图像大小，然后，将分配其自己数据缓冲区。 WIA 驱动程序将读取[ **WIA\_IPA\_缓冲区\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551527)属性并为单个带区的数据分配内存。 WIA 驱动程序可以分配任何在这里，所需的内存量，但建议的分配会保持小。

若要查看 WIA 服务是否已为该驱动程序分配内存，请*pmdtc-&gt;bClassDrvAllocBuf*标志。 如果设置为 **，则返回 TRUE**，然后 WIA 服务已为该驱动程序分配内存。 若要了解已分配的内存量，检查值*pmdtc-&gt;lBufferSize*。

若要分配你自己的内存，请使用**CoTaskMemAlloc** （Microsoft Windows SDK 文档中介绍），并使用位于指针*pmdtc-&gt;pTransferBuffer*。 （请记住，该驱动程序分配给此内存，因此驱动程序还必须释放它。）设置*pmdtc-&gt;lBufferSize*向你分配的大小。 如前文所述，此 WIA 示例驱动程序分配一个缓冲区，其大小，以字节为单位，是否等于中包含的值[ **WIA\_IPA\_缓冲区\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551527)。 然后，该驱动程序使用的内存。

下面的示例演示的实现**IWiaMiniDrv::drvAcquireItemData**方法。 此示例中可以处理这两个内存分配情况。

```cpp
HRESULT _stdcall CWIADevice::drvAcquireItemData(
  BYTE                      *pWiasContext,
  LONG                      lFlags,
  PMINIDRV_TRANSFER_CONTEXT pmdtc,
  LONG                      *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
    return E_INVALIDARG;
  }

  if (!pmdtc) {
    return E_INVALIDARG;
  }

  if (!plDevErrVal) {
    return E_INVALIDARG;
  }

  *plDevErrVal = 0;

  HRESULT hr = E_FAIL;
  LONG lBytesTransferredToApplication = 0;
  LONG lClassDrvAllocSize = 0;
  //
  // (1) Memory allocation
  //

  if (pmdtc->bClassDrvAllocBuf) {

    //
    // WIA allocated the buffer for data transfers
    //

    lClassDrvAllocSize = pmdtc->lBufferSize;
    hr = S_OK;
  } else {

    //
    // Driver allocated the buffer for data transfers
    //

    hr = wiasReadPropLong(pWiasContext, WIA_IPA_BUFFER_SIZE, &lClassDrvAllocSize,NULL,TRUE);
    if (FAILED(hr)) {

      //
      // no memory was allocated, here so we can return early
      //

      return hr;
    }

    //
    // allocate memory of WIA_IPA_BUFFER_SIZE (own min buffer size)
    //

    pmdtc->pTransferBuffer = (PBYTE) CoTaskMemAlloc(lClassDrvAllocSize);
    if (!pmdtc->pTransferBuffer) {

      //
      // no memory was allocated, here so we can return early
      //

      return E_OUTOFMEMORY;
    }

    //
    // set the lBufferSize member
    //

    pmdtc->lBufferSize = lClassDrvAllocSize;
  }

  //
  // (2) Gather all information about data transfer settings and
  //     calculate the total data amount to transfer
  //

  if (hr == S_OK) {
    //
    // WIA service will populate the MINIDRV_TRANSFER_CONTEXT by reading the WIA properties.
    //
    // The following values will be written as a result of the 
    // wiasGetImageInformation() call
    //
    // pmdtc->lWidthInPixels
    // pmdtc->lLines
    // pmdtc->lDepth
    // pmdtc->lXRes
    // pmdtc->lYRes
    // pmdtc->lCompression
    // pmdtc->lItemSize
    // pmdtc->guidFormatID
    // pmdtc->tymed
    //
    // if the FORMAT is set to BMP or MEMORYBMP, the
    // following values will also be set automatically
    //
    // pmdtc->cbWidthInBytes
    // pmdtc->lImageSize
    // pmdtc->lHeaderSize
    // pmdtc->lItemSize (will be updated using the known image format information)
    //

    hr = wiasGetImageInformation(pWiasContext,0,pmdtc);
    if (hr == S_OK) {

      //
      // (3) Send the image data to the application
      //

      LONG lDepth = 0;
      hr = wiasReadPropLong(pWiasContext, WIA_IPA_DEPTH, &lDepth,NULL,TRUE);
      if (hr == S_OK) {

        LONG lPixelsPerLine = 0;
        hr = wiasReadPropLong(pWiasContext, WIA_IPA_PIXELS_PER_LINE, &lPixelsPerLine,NULL,TRUE);
        if (hr == S_OK) {

            LONG lBytesPerLineRaw     = ((lPixelsPerLine * lDepth) + 7) / 8;
            LONG lBytesPerLineAligned = (lPixelsPerLine * lDepth) + 31;
            lBytesPerLineAligned      = (lBytesPerLineAligned / 8) & 0xfffffffc;
            LONG lTotalImageBytes     = pmdtc->lImageSize + pmdtc->lHeaderSize;
            LONG lBytesReceived       = pmdtc->lHeaderSize;
            lBytesTransferredToApplication = 0;
            pmdtc->cbOffset = 0;

            while ((lBytesReceived)) {

              LONG lPercentComplete = (LONG)(((float)lBytesTransferredToApplication/(float)lTotalImageBytes) * 100.0f);
              switch (pmdtc->tymed) {
              case TYMED_MULTIPAGE_CALLBACK:
              case TYMED_CALLBACK:
                {
                  hr = pmdtc->pIWiaMiniDrvCallBack->MiniDrvCallback(IT_MSG_DATA,IT_STATUS_TRANSFER_TO_CLIENT,
                                                                  lPercentComplete,pmdtc->cbOffset,lBytesReceived,pmdtc,0);
                pmdtc->cbOffset += lBytesReceived;
                lBytesTransferredToApplication += lBytesReceived;
           }
            break;
          case TYMED_MULTIPAGE_FILE:
          case TYMED_FILE:
            {
                //
                // lItemSize is the amount that wiasWriteBufToFile will write to FILE
                //

                pmdtc->lItemSize = lBytesReceived;
                hr = wiasWriteBufToFile(0,pmdtc);
                if (FAILED(hr)) {
                    break;
                }

                hr = pmdtc->pIWiaMiniDrvCallBack->MiniDrvCallback(IT_MSG_STATUS,IT_STATUS_TRANSFER_TO_CLIENT,
                                                                  lPercentComplete,0,0,NULL,0);
                lBytesTransferredToApplication += lBytesReceived;
              }
              break;
          default:
              {
          hr = E_FAIL;
              }
              break;
          }

          //
          // scan from device, requesting ytesToReadFromDevice
          //

          LONG lBytesRemainingToTransfer = (lTotalImageBytes - lBytesTransferredToApplication);
          if (lBytesRemainingToTransfer <= 0) {
              break;
            }

            //
            // calculate number of bytes to request from device
            //

            LONG lBytesToReadFromDevice = (lBytesRemainingToTransfer > pmdtc->lBufferSize) ? pmdtc->lBufferSize : lBytesRemainingToTransfer;

            // RAW data request
            lBytesToReadFromDevice = (lBytesToReadFromDevice / lBytesPerLineAligned) * lBytesPerLineRaw;

            // Aligned data request
            // lBytesToReadFromDevice = (lBytesToReadFromDevice / lBytesPerLineAligned) * lBytesPerLineAligned;

            if ((hr == S_FALSE)||FAILED(hr)) {

              //
              // user canceled or the callback failed for some reason
              //

              break;
            }

            //
            // request byte amount from device
            //

            hr = GetDataFromMyDevice(pmdtc->pTransferBuffer, lBytesToReadFromDevice, (DWORD*)&lBytesReceived);
            if (FAILED(hr)) {
                break;
            }

            //
            // this device returns raw data.  If your device does this too, then you should call the AlignInPlace
            // helper function to align the data.
            //

            lBytesReceived = AlignMyRawData(pmdtc->pTransferBuffer,lBytesReceived,lBytesPerLineAligned,lBytesPerLineRaw);

          } // while ((lBytesReceived))
        }
      }
    }
  }

  //
  // free any allocated memory for buffers
  //

  if (!pmdtc->bClassDrvAllocBuf) {
    CoTaskMemFree(pmdtc->pTransferBuffer);
    pmdtc->pTransferBuffer = NULL;
    pmdtc->lBufferSize = 0;
  }

  return hr;
}
```

 

 




