---
title: 为数据分配内存
description: 为数据分配内存
ms.assetid: 15df5616-ddce-44ec-bd10-65cae0d95cf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c85eeb041a5f53b999f86ffd7ed66dbcecfca3f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840900"
---
# <a name="allocating-memory-for-data"></a>为数据分配内存





WIA 服务依赖于 MINIDRV 中提供的信息[ **\_传输\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)结构来执行适当的数据传输。 此结构中与 WIA 微型驱动程序相关的成员包括：

**bClassDrvAllocBuf** − WIA 服务分配布尔值。

**pTransferBuffer** −指向为传输的数据分配的内存的指针。

**lBufferSize** − **pTransferBuffer**成员指向的内存大小。

如果 MINIDRV\_\_传输的**bClassDrvAllocBuf**成员设置为**TRUE**，则 WIA 服务为微型驱动程序分配内存。 如果**bClassDrvAllocBuf**成员设置为**FALSE**，则 WIA 服务不会为微型驱动程序分配任何内存。

微型驱动程序应使用**CoTaskMemAlloc**函数（如 Microsoft Windows SDK 文档中所述）分配内存。 然后，微型驱动程序应将指针存储在**pTransferBuffer**中的内存位置，并将内存大小存储在**lBufferSize**中的内存大小（以字节为单位）。

仅当[**wia\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)属性设置为 TYMED\_FILE or TYMED\_多页\_文件，并且[**WIA\_IPA\_ITEM\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)属性设置为零时，才将**bClassDrvAllocBuff**成员设置为**FALSE** 。

微型驱动程序必须注意不要 overfill **pTransferBuffer**成员指向的缓冲区。 可以通过写入小于或等于**lBufferSize**成员中存储的值的数据来避免这种情况。

### <a name="enhancing-data-transfer-performance-by-using-minimum-buffer-size"></a>使用最小缓冲区大小增强数据传输性能

WIA 微型驱动程序可以通过设置[**WIA\_IPA\_项\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)和[**WIA\_IPA\_缓存\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)属性，来控制数据传输期间使用的内存量。

WIA 应用程序使用 WIA\_IPA\_BUFFER\_大小属性来确定内存传输期间请求的最小传输缓冲区大小。 此值越大，请求的带区大小就越大。 如果 WIA 应用程序请求的缓冲区大小小于 WIA\_IPA\_BUFFER\_SIZE 属性中的值，则 WIA 服务将忽略此请求的大小并向 wia 微型驱动程序请求 IPA\_缓冲区大小为\_缓冲区大小的\_缓冲区。 WIA 服务始终为至少为 WIA\_IPA\_缓冲区的缓冲区请求 WIA，\_大小为字节。

**请注意**   WIA\_IPA\_BUFFER\_SIZE 属性包含的值为应用程序可以在任何给定时间请求的最小数据量。 缓冲区大小越大，请求的数量越大。 太小的缓冲区大小会降低数据传输的性能。

 

建议将 WIA\_IPA\_BUFFER\_SIZE 属性设置为合理的大小，以允许设备以高效速率传输数据。 为此，请平衡设备的请求数（缓冲区大小不太小）和设备的耗时请求数（缓冲区太大），以确保最佳性能。

如果 WIA 微型驱动程序可以传输数据，则应将[**wia\_IPA\_项\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)属性设置为零。 如果传输类型为 TYMED\_文件或 TYMED\_多页\_文件，则微型驱动程序负责为要传递到写入文件的 WIA 服务函数的数据缓冲区分配内存。 这会在[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法的实现中提供一致性。

当 WIA 服务打算将数据从设备传输到应用程序时，会调用[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法。 WIA 驱动程序应通过读取[**MINIDRV\_传输\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)的**tymed**成员来确定应用程序正在尝试的传输类型（通过 WIA 服务）：

应用程序设置的**tymed**成员可以具有以下四个值之一：

<a href="" id="tymed-file"></a>TYMED\_文件  
将数据传输到文件。

<a href="" id="tymed-multipage-file"></a>TYMED\_多页\_文件  
将数据传输到多页文件格式。

<a href="" id="tymed-callback"></a>TYMED\_回调  
将数据传输到内存。

<a href="" id="tymed-multipage-callback"></a>TYMED\_多页\_回调  
将多个数据页传输到内存。

不同的 TYMED 设置 XXX\_回调和 XXX\_文件更改调用应用程序的回调接口的使用情况。

### <a href="" id="tymed-callback-and-tymed-multipage-callback"></a>TYMED\_回调和 TYMED\_多页\_回调

对于内存传输，请发出[**IWiaMiniDrvCallBack：： MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)回调：

（*pmdtc-&gt;pIWiaMiniDrvCallBack-* 在下面的示例代码中&gt;MiniDrvCallback）

使用以下值进行回调：

<a href="" id="it-msg-data"></a>它\_MSG\_数据  
驱动程序正在传输数据。

<a href="" id="it-status-transfer-to-client"></a>它\_状态\_将\_传输到\_客户端  
数据传输消息。

<a href="" id="lpercentcomplete"></a>*lPercentComplete*  
已完成的传输的百分比。

<a href="" id="pmdtc--cboffset"></a>*pmdtc-&gt;cbOffset*  
将此更新到应用程序应将下一个数据块写入到的当前位置。

<a href="" id="lbytesreceived"></a>*lBytesReceived*  
要发送到应用程序的数据块区中的字节数。

<a href="" id="pmdtc"></a>*pmdtc*  
指向[**MINIDRV\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)的指针\_包含数据传输值的上下文结构。

### <a href="" id="tymed-file-and-tymed-multipage-file"></a>TYMED\_文件和 TYMED\_多页\_文件

对于文件传输，请发出[**IWiaMiniDrvCallBack：： MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)回调：：

（*pmdtc-&gt;pIWiaMiniDrvCallBack-* 在下面的示例代码中&gt;MiniDrvCallback）

使用以下值进行回调。

<a href="" id="it-msg-status"></a>\_消息\_状态  
驱动程序仅发送状态（无数据）。

<a href="" id="it-status-transfer-to-client"></a>它\_状态\_将\_传输到\_客户端  
数据传输消息。

<a href="" id="lpercentcomplete"></a>*lPercentComplete*  
已完成的传输的百分比。

如果 MINIDRV\_\_传输的**ItemSize**成员设置为零，则这将向应用程序指示 WIA 驱动程序不知道产生的图像大小，然后将分配其自己的数据缓冲区。 WIA 驱动程序将读取[**WIA\_IPA\_BUFFER\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)属性，并为单条数据分配内存。 WIA 驱动程序可以在此处分配任何所需的内存量，但建议将分配保存为小。

若要查看 WIA 服务是否为驱动程序分配了内存，请检查*pmdtc-&gt;bClassDrvAllocBuf*标志。 如果设置为**TRUE**，则 WIA 服务已为驱动程序分配内存。 若要查看分配的内存量，请检查*pmdtc-&gt;lBufferSize*中的值。

若要分配自己的内存，请使用**CoTaskMemAlloc** （如 Microsoft Windows SDK 文档中所述），并使用*Pmdtc-&gt;pTransferBuffer*中的指针。 （请记住，驱动程序分配了此内存，因此驱动程序还必须释放它。）将 *&gt;Pmdtc lBufferSize*设置为分配的大小。 如前所述，此 WIA 示例驱动程序分配一个缓冲区，该缓冲区的大小（以字节为单位）等于[**WIA\_IPA\_缓冲区\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)中包含的值。 然后，驱动程序将使用该内存。

下面的示例演示**IWiaMiniDrv：:D rvacquireitemdata**方法的实现。 此示例可以处理两个内存分配情况。

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

 

 




