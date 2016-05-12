---
title: Messages
keywords: hotel-push, messages
sidebar: mydoc_sidebar
permalink: /developer-documentation/hotel-push/messages
---

List of messages with OTA xsd structure used:

  -------------------------------------------------------------------------
  Method          OTA RQ       OTA RS      Type  Description
  --------------- ------------ ----------- ----- --------------------------
  HotelRatePlanIn OTA\_HotelRa OTA\_HotelR Retri Retrieve static
  ventoryRetrieve tePlanRQ     atePlanRS   eve   information of hotel
                                                 seller inventory

  HotelRatePlanRe OTA\_HotelRa OTA\_HotelR Retri Retrieve rates of hotel
  trieve          tePlanRQ     atePlanRS   eve   seller

  HotelAvailRetri OTA\_HotelAv OTA\_HotelA Retri Retrieve availability of
  eve             ailGetRQ     vailGetRS   eve   hotel seller

  HotelResRetriev OTA\_ReadRQ  OTA\_HotelR Retri Retrieve reservations from
  e                            esRS        eve   user seller

  HotelRatePlanNo OTA\_HotelRa OTA\_HotelR Notif Notify rates to hotel
  tif             tePlanNotifR atePlanNoti y     seller
                  Q            fRS               

  HotelAvailNotif OTA\_HotelAv OTA\_HotelA Notif Notify availability to
                  ailNotifRQ   vailNotifRS y     hotel seller

  HotelResRetriev OTA\_HotelRe OTA\_HotelR Retri Retrieve reservations from
  e               sRetrieveRQ  esRetrieveR eve   user seller
                               S                 
  -------------------------------------------------------------------------

**Contents:**

> maxdepth
>
> :   3
>
> numbered
>
> :   
>
> Typical Exchange Message Scenario
> \<./messages-files/typical-scenario.rst\> Retrieve Messages
> \<./messages-files/retrieve-messages.rst\> Notify Messages
> \<./messages-files/notify-messages.rst\>