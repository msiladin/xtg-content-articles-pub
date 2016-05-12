---
title: ModifyValuation
keywords: hotel, data structure, modify valuation
sidebar: mydoc_sidebar
permalink: /developer-documentation/hotel/DSF/ModifyValuation
---

|

Method Goals
============

This message lets you know if it is possible a modify, and new price of
that.

|

Request Format
==============

The request require the reservation and all modifications will be apply
( these will depend on what is specified in the *StaticConfiguration* )

|

Response Format
===============

The XML returned contains a simulation of the new booking.

|

Remarks
=======

The maximum time, that is permitted in our system, before the connection
is closed, is of **180000** milliseconds.

|

ModifyValuationRQ Example
=========================

    <ModifyValuationRQ>
        <OnRequest>false</OnRequest>
        <Nationality>ES</Nationality>
        <BlockOption>true</BlockOption>
        <Reservation>
            <Locators>
                <Client>5356342</Client>
                <Provider>MGNZ12345</Provider>
            </Locators>
            <Currency>EUR</Currency>
            <StartDate>28/01/2014</StartDate>
            <EndDate>29/01/2014</EndDate>
            <CreationDate>17/01/2014</CreationDate>
        </Reservation>
        <Modifications>
            <ModifyMealPlan></ModifyMealPlan>
            <ModifyStartDateAddDays>
                <StartDate>29/01/2014</StartDate>
            </ModifyStartDateAddDays>
            <ModifyEndDateAddDays>
                <EndDate>30/01/2014</EndDate>
            </ModifyEndDateAddDays>
             <ModifyHolder>
                <Holder name = "Test11Modify" surname = "TestSur11Modify"/>
            </ModifyHolder>
            <ModifyRoomsAddRooms>
                <Rooms>
                    <Room code = "506">
                        <PaxGuests>
                            <PaxGuest age = "30">
                                <GivenName>name1</GivenName>
                                <SurName>surname1</SurName>
                            </PaxGuest>
                            <PaxGuest age = "30">
                                <GivenName>name2</GivenName>
                                <SurName>surname2</SurName>
                            </PaxGuest>
                        </PaxGuests>
                    </Room>
                </Rooms>
            </ModifyRoomsAddRooms>
            <ModifyRoomsRemoveRooms>
                <Rooms>
                    <Room code = "500">
                        <Price currency = "EUR" amount = "36.20" binding = "false" commission = "-1"/>
                        <PaxGuests>
                            <PaxGuest age = "30">
                                <GivenName>name1</GivenName>
                                <SurName>surname1</SurName>
                            </PaxGuest>
                            <PaxGuest age = "30">
                                <GivenName>name2</GivenName>
                                <SurName>surname2</SurName>
                            </PaxGuest>
                        </PaxGuests>                        
                    </Room>
                </Rooms>
            </ModifyRoomsRemoveRooms>
        </Modifications>
    </ModifyValuationRQ>

|

ModifyValuationRQ Description
=============================

  --------------------------------------------------------------------------
  Element                Num Typ Description
                         ber e   
  ---------------------- --- --- -------------------------------------------
  ModifyValuationRQ      1       Root node.

  OnRequest              1   Boo Indicates if you want to receive the on
                             lea request options in AvailRS, as long as the
                             n   provider returns it in this call (see
                                 StaticConfiguration).

  Nationality            0.. Str Nationality of the Holder (use
                         1   ing ISO3166\_1\_alfa\_2). This informations
                                 will be mandatory depending on the
                                 provider, as long as the provider returns
                                 it in this call (see StaticConfiguration).

  BlockOption            1   Boo Indicates if you want to block the option
                             lea selected in AvailRS, as long as the
                             n   provider allow it in this call (see
                                 StaticConfiguration).

  Reservation            1       Reservation data.

  Reservation/Locators   1       Information of the locators (it is
                                 mandatory indicate one of two, or client or
                                 provider).

  Reservation/Locators/C 0.. Str Client locator.
  lient                  1   ing 

  Reservation/Locators/P 0.. Str Provider locator.
  rovider                1   ing 

  Reservation/Currency   1   Str Currency code.
                             ing 

  Reservation/StartDate  1   Str Start date of booking.
                             ing 

  Reservation/EndDate    1   Str End date of booking.
                             ing 

  Reservation/CreationDa 1   Str Creation date of booking.
  te                         ing 

  Modifications          1       Modifications.

  Modifications/ModifySt 0..     Add days of check-in.
  artDateAddDays         1       

  Modifications/ModifySt 1   Str New check-in.
  artDateAddDays/StartDa     ing 
  te                             

  Modifications/ModifySt 0..     Subtract days of check-in.
  artDateSubtractDays    1       

  Modifications/ModifySt 1   Str New check-in.
  artDateSubtractDays/St     ing 
  artDate                        

  Modifications/ModifyEn 0..     Add days of check-out.
  dDateAddDays           1       

  Modifications/ModifyEn 1   Str New check-out.
  dDateAddDays/EndDate       ing 

  Modifications/ModifyEn 0..     Subtract days of check-out.
  dtDateSubtractDays     1       

  Modifications/ModifyEn 1   Str New check-out.
  dtDateSubtractDays/End     ing 
  Date                           

  Modifications/ModifyHo 0..     Modify holder.
  lder                   1       

  Modifications/ModifyHo 1       New holder.
  lder/Holder                    

  <*@name>\*             1   Str Holder name.
                             ing 

  <*@surname>\*          1   Str Holder surname.
                             ing 

  Modifications/ModifyRo 0..     Add Rooms structure.
  omsAddRooms            1       

  Modifications/ModifyRo 1       Rooms Add.
  omsAddRooms/Rooms              

  Modifications/ModifyRo 1..     Room Add.
  omsAddRooms/Rooms/Room n       

  <*@code>\*             1   Str Room code.
                             ing 

  Modifications/ModifyRo 1       List of passenger.
  omsAddRooms/Rooms/Room         
  /PaxGuests                     

  Modifications/ModifyRo 1..     Detail of each passenger.
  omsAddRooms/Rooms/Room n       
  /PaxGuests/PaxGuest            

  <*@age>\*              1   Str Age pax.
                             ing 

  Modifications/ModifyRo 1   Str Given Name.
  omsAddRooms/Rooms/Room     ing 
  /PaxGuests/PaxGuest/Gi         
  venName                        

  Modifications/ModifyRo 1   Str Surname.
  omsAddRooms/Rooms/Room     ing 
  /PaxGuests/PaxGuest/Su         
  rName                          

  Modifications/ModifyRo 0..     Remove Rooms structure.
  omsRemoveRooms         1       

  Modifications/ModifyRo 1       Rooms Remove.
  omsRemoveRooms/Rooms           

  Modifications/ModifyRo 1..     Room Remove.
  omsRemoveRooms/Rooms/R n       
  oom                            

  <*@code>\*             1   Str Room code.
                             ing 

  Modifications/ModifyRo 1       Price Room.
  omsRemoveRooms/Rooms/R         
  oom/Price                      

  <*@currency>\*         1   Str Currency code.
                             ing 

  <*@amount>\*           1   Dec Room Amount.
                             ima 
                             l   

  <*@binding>\*          1   Boo Identifies if is the price is binding (
                             lea When true the sale price returned **must**
                             n   not be less than the price informed.

  <*@commission>\*       1   Dec Commission (-1 = not specified (will come
                             ima indicated with the provider contract), 0 =
                             l   net price, X = % of the commission that
                                 applies to the amount).

  Modifications/ModifyRo 1       List of passenger.
  omsRemoveRooms/Rooms/R         
  oom/PaxGuests                  

  Modifications/ModifyRo 1..     Detail of each passenger.
  omsRemoveRooms/Rooms/R n       
  oom/PaxGuests/PaxGuest         

  <*@age>\*              1   Str Age pax.
                             ing 

  Modifications/ModifyRo 1   Str Given Name.
  omsRemoveRooms/Rooms/R     ing 
  oom/PaxGuests/PaxGuest         
  /GivenName                     

  Modifications/ModifyRo 1   Str Surname.
  omsRemoveRooms/Rooms/R     ing 
  oom/PaxGuests/PaxGuest         
  /SurName                       
  --------------------------------------------------------------------------

|

ModifyValuationRS Example
=========================

    <ModifyValuationRS>
        <Status>OK</Status>
        <ModifyPenalty currency = "EUR" amount = "0" binding = "false" commission = "-1"/>
        <HotelReservation>
            <Remarks>The option has the following features: One Bed, Suite</Remarks>
            <PaymentOptions cash = "false" bankAcct = "false">
                <Cards>
                    <Card code = "VI"/>
                    <Card code = "AX"/>
                    <Card code = "CB"/>
                    <Card code = "DS"/>
                    <Card code = "JC"/>
                    <Card code = "CA"/>
                </Cards>
            </PaymentOptions>
            <Price currency = "EUR" amount = "86.20" binding = "false" commission = "-1"/>
        </HotelReservation>
        <Parameters>
            <Parameter key = "bd1" value = "43"/>
        </Parameters>
    </ModifyValuationRS>

|

ModifyValuationRS Description
=============================

  -------------------------------------------------------------------------
  Element   Num Type Description
            ber      
  --------- --- ---- ------------------------------------------------------
  ModifyVal 1        Root node.
  uationRS           

  Status    1        Status option (OK = available, RQ = on request).

  ModifyPen 1        Price of penalty modification.
  alty               

  <*@curren 1   Stri Currency code.
  cy>\*         ng   

  <*@amount 1   Deci Penalty Amount.
  >\*           mal  

  <*@bindin 1   Bool Identifies if is the price is binding ( When true the
  g>\*          ean  sale price returned **must** not be less than the
                     price informed.

  <*@commis 1   Deci Commission ( -1 = not specified (will come indicated
  sion>\*       mal  with the provider contract ), 0 = net price, X = % of
                     the commission that applies to the amount).

  HotelRese 1        HotelReservation.
  rvation            

  HotelRese 0.. Stri Remarks.
  rvation/R 1   ng   
  emarks             

  HotelRese 0..      New total reservation price.
  rvation/  1        
  PaymentOp          
  tions              

  <*@cash>\ 1        Boolean that indicates if it is cash or not.
  *                  

  <*@bankAc 1        Boolean that indicates if there is a bank account.
  ct>\*              

  HotelRese 0..      List of credit cards.
  rvation/  1        
  PaymentOp          
  tions/Car          
  ds                 

  HotelRese 1..      Credit card.
  rvation/  n        
  PaymentOp          
  tions/Car          
  ds/                
  Card               

  <*@Card>  1        Indicates the credit card.
  code\*             

  HotelRese 1        New total reservation price.
  rvation/P          
  rice               

  <*@curren 1   Stri Currency code.
  cy>\*         ng   

  <*@amount 1   Deci Reservation Amount.
  >\*           mal  

  <*@bindin 1   Bool Identifies if is the price is binding ( When true the
  g>\*          ean  sale price returned **must** not be less than the
                     price informed.

  <*@commis 1   Deci Commission ( -1 = not specified (will come indicated
  sion>\*       mal  with the provider contract ), 0 = net price, X = % of
                     the commission that applies to the amount).

  CancelPen 0..      New information of cancellation policies with the
  alties    1        modifications.

  <*@nonRef 1   Bool Indicate if this option is nonRefundable (true or
  undable>\     ean  false).
  *                  

  CancelPen 0..      Listing cancellation penalties.
  alties/   n        
  CancelPen          
  alty               

  CancelPen 1   Stri Number of hours prior to arrival day in which this
  alties/       ng   Cancellation policy applies.
  CancelPen          
  alty/Hour          
  sBefore            

  CancelPen 1        Contains the value to apply.
  alties/            
  CancelPen          
  alty/Pena          
  lty                

  <*@type>\ 1   Stri Type of penalty Possible values: "Noches" (nights) ,
  *             ng   "Porcentaje" (percentage) ,"Importe" (price value).

  <*@curren 1   Stri Currency code.
  cy>\*         ng   

  Parameter 0..      Parameters for additional information.
  s         1        

  Parameter 1..      List of parameter.
  s/Paramet n        
  er                 

  <*@key>\* 1   Stri Contains the keyword/Id to identify a parameter.
                ng   

  <*@value> 1   Stri Contains the value of the parameter.
  \*            ng   
  -------------------------------------------------------------------------

|