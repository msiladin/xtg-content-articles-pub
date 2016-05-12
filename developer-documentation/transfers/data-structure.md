---
title: Data Structure
keywords: transfers, data structure
sidebar: mydoc_sidebar
permalink: /developer-documentation/transfers/data-structure
---

The structure of the API specification follows a standard. This document
intends to explain every aspect of this structure and their fields. The
integration will have the following methods:

  --------------------------------------------------------------------------
  Method   Input     Output    Requ Description               Endpoint
                               ired                           
  -------- --------- --------- ---- ------------------------- --------------
  Availabi Availabil Availabil Yes  Makes an availability     Transfers Book
  lity     ityRQ     ityRS          search                    ing Endpoint\_

  RateRule RateRuleR RateRuleR Yes  Makes a pre-booking       Transfers Book
           Q         S                                        ing Endpoint\_

  Book     BookRQ    BookRS    Yes  Creates a booking         Transfers Book
                                                              ing Endpoint\_

  Retrieve RetrieveB RetrieveB No   Retrieves Booking details Transfers Book
  Booking  ookingRQ  ookingRS                                 ing Endpoint\_

  CancelBo CancelBoo CancelBoo No   Cancels a booking         Transfers Book
  oking    kingRQ    kingRS                                   ing Endpoint\_

  Destinat Destinati Destinati Yes  Gets a hierarchical list  Transfers Book
  ionsTree onsTreeRQ onsTreeRS      of destinations.          ing Endpoint\_

  HotelLis HotelList HotelList No   Gets a list of the hotels Transfers Book
  t        RQ        RS             with a basic information. ing Endpoint\_

  GetRates GetRatesR GetRatesR No   Gets a list of the rates  Transfers Book
           Q         S              with a basic information. ing Endpoint\_

  GetSuppl GetSupple GetSupple No   Gets a list of the        Transfers Book
  ements   mentsRQ   mentsRS        supplements with a basic  ing Endpoint\_
                                    information               

  GetSuppl Getsuppli Getsuppli No   Gets a list of the types  Transfers Book
  ierRate  erRate    erRate         of suppliers transfers    ing Endpoint\_
  Transfer Transfers Transfers      rates with a basic        
  sType    TypeRQ    TypeRS         information.              

  GetSuppl GetSuppli GetSuppli No   Gets a list of the        Transfers Book
  ier      er        er             suppliers transfers types ing Endpoint\_
  Transfer Transfers Transfers      with a basic information. 
  sType    TypeRQ    TypeRS                                   

  GetTrans GetTransf GetTransf No   Gets a list of the        Transfers Book
  fers     ers       ers            transfers types with a    ing Endpoint\_
  Types    TypesRQ   TypesRQ        basic information.        

  GetVehic GetVehicl GetVehicl No   Gets a list of the        Transfers Book
  les      esRQ      esRS           vehicles with a basic     ing Endpoint\_
                                    information.              
  --------------------------------------------------------------------------

Each request sent to the **service url** requires a node called rqXML .
Inside this node travels the current method's Input object.

The data structure will always have common elements in all objects and
the specific objects related to the operation.

|

**Data structure content:**

> maxdepth
>
> :   3
>
> numbered
>
> :   
>
> Common-Elements\<./DSF/common-elements.rst\> Avail\<./DSF/avail.rst\>
> Rate Rule\<./DSF/rate-rule.rst\> Book \<./DSF/reservation.rst\>
> Retrieve Booking \<./DSF/retrieve-booking.rst\> Cancel Booking
> \<./DSF/cancel-booking.rst\> DestinationTree
> \<./DSF/destinationtree.rst\> HotelList\<./DSF/hotel-list.rst\>
> GetRates \<./DSF/GetRates.rst\> GetSupplements
> \<./DSF/GetSupplements.rst\> GetSupplierRateTransferTypes
> \<./DSF/GetSupplierRateTransferTypes.rst\>
> GetSupplierTransferTypes\<./DSF/GetSupplierTranferTypes.rst\>
> GetTransfersTypes\<./DSF/GetTransfersTypes.rst\>
> GetVehicles\<./DSF/GetVehicles.rst\>