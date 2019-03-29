---
title: 用于处理常规或直接 OID 请求的示例样板
description: 本主题介绍用于处理常规连接或直接 OID 请求的样本代码示例
ms.assetid: 4C8297DD-C237-4437-A0B1-8CE0F3A6225B
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5e5ccc8bfaf684c6b1c765749926094b17d94e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576365"
---
# <a name="example-boilerplate-for-handling-regular-or-direct-oid-requests"></a>用于处理常规或直接 OID 请求的示例样板

本主题提供的样本代码示例用于处理常规连接或直接 OID，对请求中的示例与对比度[同步 OID 请求接口在 NDIS 6.80](synchronous-oid-request-interface-in-ndis-6-80.md)。 Windows 10 版本 1709年及更高版本上提供了同步 OID 请求接口。

```cpp
NDIS_STATUS
FilterOidRequest(
  NDIS_HANDLE     FilterModuleContext,
  PNDIS_OID_REQUEST  Request)
{
  PMS_FILTER       pFilter = (PMS_FILTER)FilterModuleContext;

  Status = NdisAllocateCloneOidRequest(pFilter->FilterHandle,
                     Request,
                     FILTER_TAG,
                    &ClonedRequest);
  if (Status != NDIS_STATUS_SUCCESS)
    return Status;

  Context = (PFILTER_REQUEST_CONTEXT)(&ClonedRequest->SourceReserved[0]);
  *Context = Request;

  ClonedRequest->RequestId = Request->RequestId;

  Status = NdisFOidRequest(pFilter->FilterHandle, ClonedRequest);

  if (Status != NDIS_STATUS_PENDING)
  {
    FilterOidRequestComplete(pFilter, ClonedRequest, Status);
    Status = NDIS_STATUS_PENDING;
  }
  return Status;
}

VOID
FilterOidRequestComplete(
  NDIS_HANDLE     FilterModuleContext,
  PNDIS_OID_REQUEST  Request,
  NDIS_STATUS     Status)
{
  PMS_FILTER             pFilter = (PMS_FILTER)FilterModuleContext;
  PNDIS_OID_REQUEST          OriginalRequest;

  Context = (PFILTER_REQUEST_CONTEXT)(&Request->SourceReserved[0]);
  OriginalRequest = (*Context);

  //
  // Copy the information from the returned request to the original request
  //
  switch(Request->RequestType)
  {
    case NdisRequestMethod:
      OriginalRequest->DATA.METHOD_INFORMATION.OutputBufferLength = Request->DATA.METHOD_INFORMATION.OutputBufferLength;
      OriginalRequest->DATA.METHOD_INFORMATION.BytesRead = Request->DATA.METHOD_INFORMATION.BytesRead;
      OriginalRequest->DATA.METHOD_INFORMATION.BytesNeeded = Request->DATA.METHOD_INFORMATION.BytesNeeded;
      OriginalRequest->DATA.METHOD_INFORMATION.BytesWritten = Request->DATA.METHOD_INFORMATION.BytesWritten;
      break;

    case NdisRequestSetInformation:
      OriginalRequest->DATA.SET_INFORMATION.BytesRead = Request->DATA.SET_INFORMATION.BytesRead;
      OriginalRequest->DATA.SET_INFORMATION.BytesNeeded = Request->DATA.SET_INFORMATION.BytesNeeded;
      break;

    case NdisRequestQueryInformation:
    case NdisRequestQueryStatistics:
    default:
      OriginalRequest->DATA.QUERY_INFORMATION.BytesWritten = Request->DATA.QUERY_INFORMATION.BytesWritten;
      OriginalRequest->DATA.QUERY_INFORMATION.BytesNeeded = Request->DATA.QUERY_INFORMATION.BytesNeeded;
      break;
  }

  NdisFreeCloneOidRequest(pFilter->FilterHandle, Request);

  NdisFOidRequestComplete(pFilter->FilterHandle, OriginalRequest, Status);
}
```

