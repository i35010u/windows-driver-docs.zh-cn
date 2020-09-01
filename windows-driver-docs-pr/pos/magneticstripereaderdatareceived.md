---
title: MagneticStripeReaderDataReceived
description: 成功的磁条读取器 (MSR) scan 事件之后，将引发 MagneticStripeReaderDataReceived 事件。
ms.assetid: 5074669c-3914-4d15-983b-d979c7f88b21
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: a5c938901621636fd06b6bf13d4e6f0f05627fdf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191917"
---
# <a name="magneticstripereaderdatareceived"></a>MagneticStripeReaderDataReceived

成功的磁条读取器 (MSR) 扫描事件之后，将引发此事件。

## <a name="syntax"></a>语法

```cpp
typedef struct _MSR_DATA_RECEIVED {
    MsrCardType CardType;
    unsigned char Track1EncryptedDataLength;
    unsigned char Track2EncryptedDataLength;
    unsigned char Track3EncryptedDataLength;
    unsigned char Track4EncryptedDataLength;
    unsigned char Track1EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track2EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track3EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track4EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track1MaskedDataLength;
    unsigned char Track2MaskedDataLength;
    unsigned char Track3MaskedDataLength;
    unsigned char Track4MaskedDataLength;
    unsigned char Track1MaskedData[MSR_TRACK_SIZE];
    unsigned char Track2MaskedData[MSR_TRACK_SIZE];
    unsigned char Track3MaskedData[MSR_TRACK_SIZE];
    unsigned char Track4MaskedData[MSR_TRACK_SIZE];
    unsigned char Track1DiscretionaryDataLength;
    unsigned char Track2DiscretionaryDataLength;
    unsigned char Track1DiscretionaryData[MSR_TRACK_SIZE];
    unsigned char Track2DiscretionaryData[MSR_TRACK_SIZE];
    unsigned char CardAuthenicationDataLength; // Length of data after encryption, may include padding.
    unsigned char CardAuthenticationDataAbsoluteLength; // Length of data before encryption, may be needed to strip padding on decryption.
    unsigned char CardAuthenicationData[MSR_CARD_AUTHENTICATION_DATA_SIZE];
    unsigned char AdditionalSecurityInformationLength;
    unsigned char AdditionalSecurityInformation[MSR_ADDITIONAL_SECURITY_INFORMATION_SIZE];
} MSR_DATA_RECEIVED, *PMSR_DATA_RECEIVED;
```

下表显示此事件的数据缓冲区的内存布局。

| 内存值 | 说明 
|---|---|
| 0x00000008                                                          | **事件 = PosEventType：： MagneticStripeReaderDataReceived**                                                                       |
| UINT32                                                              | **DataLength** = Sizeof (**PosEventDataHeader**) + sizeof (** \_ \_ 收到 MSR 数据**)                                                      |
| 32位 MsrCardType                                                  | [MsrCardType](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                                                                                                        |
| unsigned char                                                       | **Track1EncryptedDataLength** -在 [MsrDataEncryption](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption) 为 **MsrDataEncryption \_ None**时，将始终为零 (0) 。 |
| unsigned char                                                       | **Track2EncryptedDataLength** -在 [MsrDataEncryption](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption) 为 **MsrDataEncryption \_ None**时，将始终为零 (0) 。 |
| unsigned char                                                       | **Track3EncryptedDataLength** -在 [MsrDataEncryption](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption) 为 **MsrDataEncryption \_ None**时，将始终为零 (0) 。 |
| unsigned char                                                       | **Track4EncryptedDataLength** -在 [MsrDataEncryption](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption) 为 **MsrDataEncryption \_ None**时，将始终为零 (0) 。 |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 加密磁道1数据的**Track1EncryptedDataLength**字节                                                                         |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 加密磁道2数据的**Track2EncryptedDataLength**字节                                                                         |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 加密磁道3数据的**Track3EncryptedDataLength**字节                                                                         |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 加密磁道4数据的**Track4EncryptedDataLength**字节                                                                         |
| unsigned char                                                       | **Track1MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track2MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track3MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track4MaskedDataLength**                                                                                                            |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 屏蔽轨迹1数据的**Track1MaskedDataLength**字节数                                                                               |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | **Track2MaskedDataLength** bytes of 遮掩 track 2 数据                                                                               |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | **Track3MaskedDataLength** bytes of 遮掩 track 3 数据                                                                               |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | **Track4MaskedDataLength** bytes of 遮掩 track 4 数据                                                                               |
| unsigned char                                                       | **Track1DiscretionaryDataLength** –如果 **MagneticStripeReaderIsDecodeDataEnabled** 为 false，将始终为零 (0) 。                |
| unsigned char                                                       | **Track2DiscretionaryDataLength**–如果 **MagneticStripeReaderIsDecodeDataEnabled** 为 false，将始终为零 (0) 。                 |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 任意磁道1数据的**Track1DiscretionaryDataLength**字节数                                                                 |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 随机跟踪2数据的**Track2DiscretionaryDataLength**字节数                                                                 |
| unsigned char                                                       | **CardAuthenicationDataLength** -加密数据的长度（以字节为单位），包括填充                                            |
| unsigned char                                                       | **CardAuthenticationDataAbsoluteLength** -未加密数据的长度（以字节为单位） (你可能需要在解密过程中去除填充)   |
| 无符号字符 \[ MSR \_ 附加的 \_ 安全 \_ 信息 \_ 数据 \_ 大小\] | 卡身份验证数据的**CardAuthenticationDataAbsoluteLength**字节数                                                            |
| unsigned char                                                       | **AdditionalSecurityInformationLength**                                                                                               |
| 无符号字符 \[ MSR \_ 附加的 \_ 安全 \_ 信息 \_ 大小\]       | 额外安全信息的**AdditionalSecurityInformationLength**字节数                                                      |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface