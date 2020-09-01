---
title: 为数据分配内存
description: 为数据分配内存
ms.assetid: 15df5616-ddce-44ec-bd10-65cae0d95cf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e34f3c54d994fa21fa5e1542d732d937f07b19d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191971"
---
# <a name="allocating-memory-for-data"></a>为数据分配内存





WIA 服务依赖于 [**MINIDRV \_ 传输 \_ 上下文**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context) 结构中提供的信息来执行适当的数据传输。 此结构中与 WIA 微型驱动程序相关的成员包括：

**bClassDrvAllocBuf** − WIA 服务分配布尔值。

**pTransferBuffer** −指向为传输的数据分配的内存的指针。

**lBufferSize** − **pTransferBuffer** 成员指向的内存大小。

如果 MINIDRV **bClassDrvAllocBuf** \_ 传输上下文结构的 bClassDrvAllocBuf 成员 \_ 设置为**TRUE**，则 WIA 服务为微型驱动程序分配内存。 如果 **bClassDrvAllocBuf** 成员设置为 **FALSE**，则 WIA 服务不会为微型驱动程序分配任何内存。

微型驱动程序应使用 Microsoft Windows SDK 文档) 中所述的 **CoTaskMemAlloc** 函数 (分配内存。 然后，微型驱动程序应将指针存储在 **pTransferBuffer** 中的内存位置，并以字节为单位存储 **lBufferSize** (的内存大小) 。

仅当[**wia \_ IPA \_ TYMED**](./wia-ipa-tymed.md)属性设置为 TYMED **bClassDrvAllocBuff** file **FALSE** \_ 或 TYMED \_ 多页 \_ 文件，并且[**wia \_ IPA \_ ITEM \_ SIZE**](./wia-ipa-item-size.md)属性设置为零时，才将 bClassDrvAllocBuff 成员设置为 FALSE。

微型驱动程序必须注意不要 overfill **pTransferBuffer** 成员指向的缓冲区。 可以通过写入小于或等于 **lBufferSize** 成员中存储的值的数据来避免这种情况。

### <a name="enhancing-data-transfer-performance-by-using-minimum-buffer-size"></a>使用最小缓冲区大小增强数据传输性能

WIA 微型驱动程序可以通过设置 [**wia \_ IPA \_ 项 \_ 大小**](./wia-ipa-item-size.md) 和 [**wia \_ IPA \_ 缓冲区 \_ 大小**](./wia-ipa-buffer-size.md) 属性来控制在数据传输过程中使用的内存量。

WIA 应用程序使用 WIA \_ IPA \_ buffer \_ size 属性来确定要在内存传输过程中请求的最小传输缓冲区大小。 此值越大，请求的带区大小就越大。 如果 WIA 应用程序请求的缓冲区大小小于 "WIA \_ IPA buffer size" 属性中的值 \_ \_ ，wia 服务将忽略此请求的大小，并向 wia 微型驱动程序请求为 wia \_ IPA \_ 缓冲区 \_ 大小字节大小的缓冲区。 WIA 服务始终为至少为 WIA \_ IPA \_ 缓冲区 \_ 大小字节大小的缓冲区请求 wia 微型驱动程序。

**注意**   WIA \_ IPA \_ BUFFER \_ SIZE 属性包含的值是应用程序可以在任何给定时间请求的最小数据量。 缓冲区大小越大，请求的数量越大。 太小的缓冲区大小会降低数据传输的性能。

 

建议将 "WIA \_ IPA \_ BUFFER size" 属性设置 \_ 为合理的大小，以允许设备以高效速率传输数据。 为此，请平衡 (缓冲区大小不太太小) 的请求数，以及 (缓冲区太) 长的时间，以便确保最佳性能。

如果 WIA 微型驱动程序可以传输数据，则应将 " [**wia \_ IPA \_ ITEM \_ SIZE**](./wia-ipa-item-size.md) " 属性设置为零。 如果传输类型为 "TYMED \_ file" 或 "TYMED \_ 多页" \_ 文件，则微型驱动程序负责为要传递给写入到文件的 WIA 服务函数的数据缓冲区分配内存。 这会在 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法的实现中提供一致性。

当 WIA 服务打算将数据从设备传输到应用程序时，会调用 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法。 WIA 驱动程序应通过读取[**MINIDRV \_ 传输 \_ 上下文**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)的**tymed**成员来确定哪些类型的传输 (通过 WIA 服务) 应用程序正在尝试：

应用程序设置的 **tymed** 成员可以具有以下四个值之一：

<a href="" id="tymed-file"></a>TYMED \_ 文件  
将数据传输到文件。

<a href="" id="tymed-multipage-file"></a>TYMED \_ 多页 \_ 文件  
将数据传输到多页文件格式。

<a href="" id="tymed-callback"></a>TYMED \_ 回调  
将数据传输到内存。

<a href="" id="tymed-multipage-callback"></a>TYMED \_ 多页 \_ 回调  
将多个数据页传输到内存。

不同的 TYMED 设置 XXX \_ 回调和 XXX \_ 文件将更改调用应用程序的回调接口的使用情况。

### <a name="tymed_callback-and-tymed_multipage_callback"></a><a href="" id="tymed-callback-and-tymed-multipage-callback"></a>TYMED \_ 回调和 TYMED \_ 多页 \_ 回调

对于内存传输，请发出 [**IWiaMiniDrvCallBack：： MiniDrvCallback**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback) 回调：

 (下面的示例源代码中的 * &gt; pIWiaMiniDrvCallBack- &gt; MiniDrvCallback*) 

使用以下值进行回调：

<a href="" id="it-msg-data"></a>IT \_ 消息 \_ 数据  
驱动程序正在传输数据。

<a href="" id="it-status-transfer-to-client"></a>IT \_ 状态 \_ 转移 \_ 到 \_ 客户端  
数据传输消息。

<a href="" id="lpercentcomplete"></a>*lPercentComplete*  
已完成的传输的百分比。

<a href="" id="pmdtc--cboffset"></a>*pmdtc- &gt; cbOffset*  
将此更新到应用程序应将下一个数据块写入到的当前位置。

<a href="" id="lbytesreceived"></a>*lBytesReceived*  
要发送到应用程序的数据块区中的字节数。

<a href="" id="pmdtc"></a>*pmdtc*  
指向包含数据传输值的 [**MINIDRV \_ 传输 \_ 上下文**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context) 结构的指针。

### <a name="tymed_file-and-tymed_multipage_file"></a><a href="" id="tymed-file-and-tymed-multipage-file"></a>TYMED \_ 文件和 TYMED \_ 多页 \_ 文件

对于文件传输，请发出 [**IWiaMiniDrvCallBack：： MiniDrvCallback**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback) 回调：：

 (下面的示例源代码中的 * &gt; pIWiaMiniDrvCallBack- &gt; MiniDrvCallback*) 

使用以下值进行回调。

<a href="" id="it-msg-status"></a>IT \_ 消息 \_ 状态  
驱动程序仅发送状态 (没有) 的数据。

<a href="" id="it-status-transfer-to-client"></a>IT \_ 状态 \_ 转移 \_ 到 \_ 客户端  
数据传输消息。

<a href="" id="lpercentcomplete"></a>*lPercentComplete*  
已完成的传输的百分比。

如果 MINIDRV **ItemSize** \_ 传输上下文结构的 ItemSize 成员 \_ 设置为零，则表示该应用程序，WIA 驱动程序并不知道产生的图像大小，然后将分配其自己的数据缓冲区。 WIA 驱动程序将读取 " [**wia \_ IPA \_ BUFFER \_ SIZE**](./wia-ipa-buffer-size.md) " 属性，并为单条数据分配内存。 WIA 驱动程序可以在此处分配任何所需的内存量，但建议将分配保存为小。

若要查看 WIA 服务是否为驱动程序分配了内存，请检查 *pmdtc- &gt; bClassDrvAllocBuf* 标志。 如果设置为 **TRUE**，则 WIA 服务已为驱动程序分配内存。 若要查看分配的内存量，请检查 *pmdtc- &gt; lBufferSize*中的值。

若要分配自己的内存，请使用 Microsoft Windows SDK 文档) 中所述的 **CoTaskMemAlloc** (，并使用位于 *pmdtc- &gt; pTransferBuffer*中的指针。  (请记住，驱动程序分配了此内存，因此驱动程序还必须释放它。 ) 将 *pmdtc- &gt; lBufferSize* 设置为分配的大小。 如前所述，此 WIA 示例驱动程序分配一个缓冲区，该缓冲区的大小（以字节为单位）等于 [**WIA \_ IPA \_ 缓冲区 \_ 大小**](./wia-ipa-buffer-size.md)中包含的值。 然后，驱动程序将使用该内存。

下面的示例演示 **IWiaMiniDrv：:D rvacquireitemdata** 方法的实现。 此示例可以处理两个内存分配情况。

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

 

