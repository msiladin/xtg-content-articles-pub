---
title: Retrieve Messages
keywords: hotel-push, messages, messages files, retrieve messages
sidebar: mydoc_sidebar
permalink: /developer-documentation/hotel-push/messages-files/retrieve-messages
---

Providers requests Sellers to retrieve data (Negotiation is started by
Providers).

|

HotelRatePlanInventoryRetrieve
==============================

Providers will send an HotelRatePlanInventoryRetrieveRQ message to
retrieve a list of hotels, rates and rooms and their configurations. XTG
will return a list of all active rooms and configurations.

|

HotelRatePlanInventoryRetrieveRQ
================================

:

    <HotelRatePlanInventoryRetrieve>
      <request PrimaryLangID = "ES">
        <POS>
          <Source>
            <RequestorID ID = "Provider1"/>
            <BookingChannel>
              <CompanyName Code = "ClientTravelAgency1"/>
            </BookingChannel>
            <TPA_Extensions>
              <Param key = "onlyActive" value = "0"/>
            </TPA_Extensions>
          </Source>
        </POS>
        <RatePlans>
          <RatePlan>
            <HotelRef HotelCode = "1"/>
          </RatePlan>
        </RatePlans>
      </request>
    </HotelRatePlanInventoryRetrieve>

  -------------------------------------------------------------------------
  Element     Num Typ Description
              ber e   
  ----------- --- --- -----------------------------------------------------
  HotelRatePl 1       Root Node
  an/request          

  <*@PrimaryL 1   Str ISO Code Language
  angID>\*        ing 

  POS/Source/ 0..     Optional, empty only active inventory will be
  TPA\_Extens 1       recieved.
  ions                

  Param       1       

  <*@key>\*   1   Str onlyActive
                  ing 

  <*@value>\* 1   Str 1 - You will recieve all active inventory data. 0 -
                  ing Active and deactivated inventory will be recieved.
                      (Same case than wihout TPA\_Extensions node.)

  RatePlans/R 0..     Contains hotel filter
  atePlan/Hot 1       
  elRef               

  <*@HotelCod 0.. Str If the hotel is not specified, it returns Rooms and
  e>\*        1   ing Rates of all user’s hotels.
  -------------------------------------------------------------------------

|

HotelRatePlanInventoryRetrieveRS
================================

**Example for RatePlan**

:

    <HotelRatePlanInventoryRetrieveResponse xmlns = "http://schemas.xmltravelgate.com/hubpush/provider/2012/10">
      <HotelRatePlanInventoryRetrieveResult Version = "0">
        <Success xmlns = "http://www.opentravel.org/OTA/2003/05"/>
        <RatePlans HotelCode = "1" HotelName = "Hotel Travelgate" xmlns = "http://www.opentravel.org/OTA/2003/05">
          <RatePlan RatePlanCode = "PACK" RatePlanType = "11" YieldableIndicator = "false" CurrencyCode = "EUR" RatePlanStatusType = "Active" Start = "2016-01-01" End = "2016-05-01">
            <BookingRules>
              <BookingRule Code = "1 Noche">
                <CancelPenalties>
                  <CancelPenalty NonRefundable = "false">
                    <Deadline OffsetTimeUnit = "Day" OffsetUnitMultiplier = "1" OffsetDropTime = "BeforeArrival"/>
                    <AmountPercent NmbrOfNights = "1,00"/>
                  </CancelPenalty>
                </CancelPenalties>
              </BookingRule>
              <BookingRule>
                <Viewerships>
                  <Viewership>
                    <LocationCodes LocationCodesInclusive = "true">
                      <LocationCode CountryCode = "ES"/>
                    </LocationCodes>
                  </Viewership>
                  <Viewership>
                    <LocationCodes LocationCodesInclusive = "false"/>
                  </Viewership>
                </Viewerships>
              </BookingRule>
            </BookingRules>
            <Description>
              <Text>Packaged Rate</Text>
            </Description>
            <Rates>
              <Rate>
                <AdditionalGuestAmounts>
                  <AdditionalGuestAmount AgeQualifyingCode = "8" MaxAge = "12"/>
                  <AdditionalGuestAmount AgeQualifyingCode = "8" MaxAge = "12"/>
                  <AdditionalGuestAmount AgeQualifyingCode = "7" MaxAge = "7"/>
                </AdditionalGuestAmounts>
                <PaymentPolicies>
                  <GuaranteePayment PaymentCode="MerchantPayment"/>
                  <GuaranteePayment PaymentCode="DirectPayment">
                    <AcceptedPayments>
                      <AcceptedPayment>
                        <PaymentCard CardCode = "VI" />
                      </AcceptedPayment>
                      <AcceptedPayment>
                        <PaymentCard>
                          <PaymentCard CardCode = "CA" />
                        </PaymentCard>
                      </AcceptedPayment>
                    </AcceptedPayments>
                  </GuaranteePayment>
                </PaymentPolicies>
                <MealsIncluded MealPlanCodes = "8"/>
              </Rate>
            </Rates>
            <SellableProducts>
              <SellableProduct InvCode = "STD1" InvType = "ROOM" InvStatusType = "Active" InvTypeCode="ROOMSTD1">
                <GuestRoom>
                  <Quantities StandardNumBeds = "2"/>
                  <Occupancy MinOccupancy = "2" MaxOccupancy = "2" AgeQualifyingCode = "10"/>
                  <Occupancy MinOccupancy = "1" MaxOccupancy = "1" AgeQualifyingCode = "8"/>
                  <Description>
                    <Text>Standard</Text>
                  </Description>
                </GuestRoom>
              </SellableProduct>
              <SellableProduct InvCode = "STD2" InvType = "ROOM" InvStatusType = "Deactivated" InvTypeCode="">
                <GuestRoom>
                  <Quantities StandardNumBeds = "2"/>
                  <Occupancy MinOccupancy = "2" MaxOccupancy = "2" AgeQualifyingCode = "10"/>
                  <Occupancy MinOccupancy = "1" MaxOccupancy = "1" AgeQualifyingCode = "8"/>
                  <Description>
                    <Text>Standard</Text>
                  </Description>
                </GuestRoom>
              </SellableProduct>
              <SellableProduct InvCode = "STD2" InvType = "ROOM" InvStatusType = "Deactivated" InvTypeCode="">
                <GuestRoom>
                  <Quantities StandardNumBeds = "2"/>
                  <Occupancy MinOccupancy = "2" MaxOccupancy = "2" AgeQualifyingCode = "10"/>
                  <Description>
                    <Text>Standard</Text>
                  </Description>
                </GuestRoom>
              </SellableProduct>
            </SellableProducts>
          </RatePlan>
        </RatePlans>
      </HotelRatePlanInventoryRetrieveResult>
    </HotelRatePlanInventoryRetrieveResponse>

If your Rate has information about meals included in rate, this will be
shown in MealsIncluded tag.

In previous example we receive one hotel, one rate and 2 rooms. One of
the rooms appears twice because each appearance sets the different
occupancies. STD2 room has 2 possible occupations: 2 adults + 1 child or
2 adults.

|

**Example for Derived RatePlan**

:

    <HotelRatePlanInventoryRetrieveResponse xmlns = "http://schemas.xmltravelgate.com/hubpush/provider/2012/10">
        <HotelRatePlanInventoryRetrieveResult Version = "0">
            <Success xmlns = "http://www.opentravel.org/OTA/2003/05"/>
            <RatePlans HotelCode = "1" HotelName = "Hotel Test Pruebas Travelgate " xmlns = "http://www.opentravel.org/OTA/2003/05">
                <RatePlan RatePlanCode = "DRVT" BaseRatePlanCode = "SRATE2" RatePlanStatusType = "Active">
                    <SellableProducts>
                        <SellableProduct InvCode = "TRP" InvType = "ROOM" InvStatusType = "Active">
                            <GuestRoom>
                                <Quantities StandardNumBeds = "3"/>
                                <Occupancy MinOccupancy = "3" MaxOccupancy = "3" AgeQualifyingCode = "10"/>
                                <Room RoomTypeCode = "TRP" RoomID = "44"/>
                                <Description>
                                    <Text>Triple</Text>
                                </Description>
                            </GuestRoom>
                        </SellableProduct>
                        <SellableProduct InvCode = "TRP" InvType = "ROOM" InvStatusType = "Active">
                            <GuestRoom>
                                <Quantities StandardNumBeds = "3"/>
                                <Occupancy MinOccupancy = "4" MaxOccupancy = "4" AgeQualifyingCode = "10"/>
                                <Room RoomTypeCode = "TRP" RoomID = "44"/>
                                <Description>
                                    <Text>Triple</Text>
                                </Description>
                            </GuestRoom>
                        </SellableProduct>
                        <SellableProduct InvCode = "TRP" InvType = "ROOM" InvStatusType = "Active">
                            <GuestRoom>
                                <Quantities StandardNumBeds = "3"/>
                                <Occupancy MinOccupancy = "2" MaxOccupancy = "2" AgeQualifyingCode = "10"/>
                                <Occupancy MinOccupancy = "2" MaxOccupancy = "2" AgeQualifyingCode = "8"/>
                                <Room RoomTypeCode = "TRP" RoomID = "44"/>
                                <Description>
                                    <Text>Triple</Text>
                                </Description>
                            </GuestRoom>
                        </SellableProduct>
                    </SellableProducts>
                    <Description>
                        <Text>Derivada Test</Text>
                    </Description>
                </RatePlan>
                <RatePlan RatePlanCode = "DRV" BaseRatePlanCode = "SRATE" RatePlanStatusType = "Active">
                    <BookingRules>
                        <BookingRule>
                            <CancelPenalties>
                                <CancelPenalty NonRefundable = "false">
                                    <Deadline OffsetTimeUnit = "Day" OffsetUnitMultiplier = "10" OffsetDropTime = "BeforeArrival"/>
                                    <AmountPercent Amount = "2.00"/>
                                </CancelPenalty>
                            </CancelPenalties>
                        </BookingRule>
                        <BookingRule>
                            <Viewerships>
                                <Viewership>
                                    <LocationCodes LocationCodesInclusive = "true">
                                        <LocationCode CountryCode = "ES"/>
                                    </LocationCodes>
                                </Viewership>
                                <Viewership>
                                    <LocationCodes LocationCodesInclusive = "false"/>
                                </Viewership>
                            </Viewerships>
                        </BookingRule>
                    </BookingRules>
                    <Description>
                        <Text>TarifaDerivada</Text>
                    </Description>
                </RatePlan>
            </RatePlans>
        </HotelRatePlanInventoryRetrieveResult>
    </HotelRatePlanInventoryRetrieveResponse> 

  ------------------------------------------------------------------------
  Element           Nu Typ Description
                    mb e   
                    er     
  ----------------- -- --- -----------------------------------------------
  HotelRatePlanResp 1      Root Node
  onse/HotelRatePla        
  nResult                  

  Success           0.     Should only be present if it was a successful
                    .1     response. The Errors node should not be present
                           if the Success node is present.

  RatePlans         0.     Present when sucess
                    .1     

  <*@HotelCode>\*   1  Str Hotel code whose information is provided by the
                       ing method

  <*@HotelName>\*   1  Str Hotel name
                       ing 

  RatePlans/RatePla 0.     Present when rates exists
  n                 .n     

  <*@RatePlanCode>\ 1  Str Rate plan code
  *                    ing 

  <*@RatePlanStatus 1  Str Active or Deactivated
  Type>\*              ing 

  <*@RatePlanType>\ 0. Int OTA RPT Code (11 - Package)
  *                 .1 ege 
                       r   

  <*@YieldableIndic 0. Boo Used to indicate the rate plan is subject to
  ator>\*           .1 lea yield management logic. When false, the rate
                       n   plan is not yieldable. When true or it's not
                           returned, the rate plan is yieldable.

  <*@CurrencyCode>\ 0. Str ISO Currency (EUR). Only null for derived rates
  *                 .1 ing 

  <*@Start>\*       0. Dat Start date of the rate booking window (Booking
                    .1 e   Dates for wich the rate will be available).

  <*@End>\*         0. Dat End date of the rate booking window (Booking
                    .1 e   Dates for wich the rate will be available).

  <*@Duration>\*    0. Str Duration of the rate booking window. Only
                    .1 ing present if Start and End are not. When present
                           value is always 0 and means the rate has no
                           booking window (available all dates).

  \_@BaseRatePlanCo 0. Str Rate plan code of the base rate plan. Only
  de                .1 ing returned for derived rates.

  \_@RatePlanStatus 1  Str Indicates if the rate plan is active or not for
  Type                 ing this dates. Possible values: "Active",
                           "Deactivated".

  RatePlans/RatePla 1      Description of rate.
  n/Description/Tex        
  t                        

  RatePlans/Booking 0.     Present if exists booking rules for the given
  Rules             .1     RatePlan.

  BookingRules/Book 1.     Booking rules.
  ingRule           .n     

  <*@Code>\*        0. Str Code of the booking rule (empty if are
                    .1 ing viewships conditions

  BookingRule/Cance 1      Cancel penalties of the current booking rule.
  lPenalties               

  CancelPenalties/C 1.     Cancel penalty.
  ancelPenalty      .n     

  <*@NonRefundable> 1  Boo Indicates if the rateplan is refundable or not.
  \*                   lea 
                       n   

  CancelPenalty/Dea 1      Contains information about the the deadline of
  dline                    the cancel penalty.

  <*@OffsetTimeUnit 1  Str Indicates the units of time that apply to the
  >\*                  ing deadline.

  <*@OffsetUnitMult 1  Int The number of units of DeadlineTimeUnit.
  iplier>\*            ege 
                       r   

  <*@OffsetDropTime 1  Str Indicating when the deadline drop time goes
  >\*                  ing into effect.

  CancelPenalty/Amo 1      Contains information about the the deadline of
  untPercent               the cancel penalty.

  <*@NmbrOfNights>\ 0. Int Number of nights that will be charged in case
  *                 .1 ege of cancellation applying the current cancel
                       r   penalty. NmbrOfNights, Percent or Amount must
                           be present.

  <*@Percent>\*     0. Dec Percent of the total amount that will be
                    .1 ima charged in case of cancellation applying the
                       l   current cancel penalty. NmbrOfNights, Percent
                           or Amount must be present.

  <*@Amount>\*      0. Dec Amount that will be charged in case of
                    .1 ima cancellation applying the current cancel
                       l   penalty. NmbrOfNights, Percent or Amount must
                           be present.

  <*@CurrencyCode>\ 0. Str Currency code of the amount. Must be present if
  *                 .1 ing amount is present.

  BookingRule/Viewe 0.     Present if exits viewerships conditions
  rships            .1     

  BookingRule/Viewe 1.     
  rships/Viewership .n     

  BookingRule/Viewe 1      One node for each viewership condition
  rships/Viewership        
  /LocationCodes           

  <*@LocationCodesI 1  Boo When its true this rate can be request for next
  nclusive>\*          lea countryCode, when false can not be requested
                       n   from this country.

  BookingRule/Viewe 0      If is missing, applies to all countryCode again
  rships/Viewership ..     the other viewership condition.
  /LocationCodes/Lo 1      
  cationCode               

  <*@CountryCode>\* 1  Str Country ISO2 code from can or can not be
                       ing requested this rate.

  RatePlan/Rate     0.     Node that contains information about the rate.
                    .1     Only null for derived rates

  Rate/AdditionalGu 1      Node that contains static information about
  estAmounts               additional guests.

  AdditionalGuestAm 1.     Static information about additional guests.
  ounts/AdditionalG .n     
  uestAmount               

  <*@AgeQualifyingC 1  Str Age qualifying code of the additional guest.
  ode>\*               ing 

  <*@MaxAge>\*      1  Int Max age not inclusive of the additional guest.
                       ege 
                       r   

  Rate/PaymentPolic 1      Node that contains the accepted payments
  ies                      information.

  PaymentPolicies/G 1.     Node that contains information about an
  uaranteePayment   .n     accepted payment.

  @PaymentCode      1      Contains the payment method accepted by the
                           rate. See Payment Type Codes list in section
                           7.6.3.

  GuaranteePayment/ 0.     Node that contains the accepted payments
  AcceptedPayments  .1     information. Only present if PaymentCode is not
                           "MerchantPayment".

  AcceptedPayments/ 1.     Node that contains the credit card accepted.
  AcceptedPayment   .n     

  AcceptedPayment/P 1.     Node that contains the credit card accepted.
  aymentCard        .n     

  @CardCode         1      String Contains the credit card code. See
                           Credit Card Codes list in section 7.6.4.

  RatePlans/RatePla 0.     Present if board is included with this rate.
  n/Rates/Rate/Meal .1     
  sIncluded                

  <*@MealPlanCodes> 1  Int OTA MPT Code.
  \*                   ege 
                       r   

  RatePlans/RatePla 0.     List of sellable products. In derived rates, if
  n/SellableProduct .1     it is not present it applies to all rooms. In
  s                        other cases, it informs the rooms that applies.

  RatePlans/RatePla 0.     Present if rooms associed with this rate.
  n/SellableProduct .n     
  s/SellableProduct        

  <*@InvCode>\*     1  Int Sellable Product Code
                       ege 
                       r   

  <*@InvType>\*     1  Int Sellable product type (ROOM)
                       ege 
                       r   

  <*@InvStatusType> 1  Str Active or Deactivated
  \*                   ing 

  <*@InvTypeCode>\* 1  Str Sellers internal Product Code. Channels can
                       ing ignore.

  RatePlans/RatePla 1.     
  n/SellableProduct .n     
  /GuestRoom               

  RatePlans/RatePla 1      
  n/SellableProduct        
  /GuestRoom/Quanti        
  ties                     

  <*@StandardNumBed 1  Int Standard occupation of room
  s>\*                 ege 
                       r   

  RatePlans/RatePla 1      
  n/SellableProduct        
  /GuestRoom/Occupa        
  ncy                      

  <*@MinOccupancy>\ 1  Int Min occupation
  *                    ege 
                       r   

  <*@MaxOccupancy>\ 1  Int Max occupation
  *                    ege 
                       r   

  <*@AgeQualifyingC 1  Int (10 - Adult,8 - Child,7 - Infant)
  ode>\*               ege 
                       r   

  RatePlans/RatePla 1  Str Room description
  n/SellableProduct    ing 
  /GuestRoom/Descri        
  ption/Text               
  ------------------------------------------------------------------------

|

HotelRatePlanRetrieve
=====================

Providers will send an HotelRatePlanRetrieveRQ message to retrieve a
complete break down of rates. XTG will return break down of hotel /
rates / rooms.

|

HotelRatePlanRetrieveRQ
=======================

:

    <HotelRatePlanRetrieve>
      <request>
        <POS>
          <Source>
            <RequestorID ID="Provider1" />
            <BookingChannel > 
              <CompanyName Code="ClientTravelAgency1"/>
            </BookingChannel>
            <TPA_Extensions>
              <Param key = "onlyActive" value = "0"/>
            </TPA_Extensions>
          </Source>
        </POS>
        <RatePlans>
          <RatePlan>
            <DateRange Start="2013-12-20" End="2013-12-25"/>
            <RatePlanCandidates>
              <RatePlanCandidate RatePlanCode="BAR"></RatePlanCandidate>
            </RatePlanCandidates>
            <HotelRef HotelCode="12" />
          </RatePlan>
        </RatePlans>
      </request>
    </HotelRatePlanRetrieve>

  --------------------------------------------------------------------------
  Element           Num Typ Description
                    ber e   
  ----------------- --- --- ------------------------------------------------
  HotelRatePlanRetr 1       Root Node
  ieve/request              

  POS/Source/TPA\_E 0..     Optional, empty only active RatePlans/Rooms will
  xtensions         1       be received.

  Param             1       

  <*@key>\*         1   Str onlyActive
                        ing 

  <*@value>\*       1   Str 1 - You will receive all active RatePlans/Rooms
                        ing data. 0 - Active and deactivated RatePlans/Rooms
                            will be received. (Same case than wihout
                            TPA\_Extensions node.)

  RatePlans/RatePla 1       Contains date filter
  n/DateRange               

  <*@Start>\*       1   Dat Start date to search rates
                        e   

  <*@End>\*         1   Dat End date to search rates
                        e   

  RatePlans/RatePla 1       Contains hotel filter
  n/HotelRef                

  <*@HotelCode>\*   1   Str Hotel date to search rates
                        ing 

  RatePlans/RatePla 0..     Contains rate filter
  n/RatePlanCandida 1       
  tes/RatePlanCandi         
  date                      

  <*@RatePlanCode>\ 1   Str Rate Plan Code to search rates
  *                     ing 
  --------------------------------------------------------------------------

|

HotelRatePlanRetrieveRS
=======================

**Example for RatePlan**

:

    <HotelRatePlanRetrieveResponse xmlns = "http://schemas.xmltravelgate.com/hubpush/provider/2012/10">
      <HotelRatePlanRetrieveResult Version = "0">
        <RatePlans HotelCode = "12" xmlns = "http://www.opentravel.org/OTA/2003/05">
          <RatePlan RatePlanType = "11" RatePlanCode = "LOWCOST" RatePlanStatusType = "Active">
            <Rates>
              <Rate Start = "2013-12-20" End = "2013-12-20">
                <BaseByGuestAmts>
                  <BaseByGuestAmt AmountAfterTax = "300.00" CurrencyCode = "EUR" NumberOfGuests = "3"/>
                </BaseByGuestAmts>
                <AdditionalGuestAmounts>
                  <AdditionalGuestAmount MaxAdditionalGuests = "1" AgeQualifyingCode = "8" Amount = "40.00" CurrencyCode = "EUR"/>
                  <AdditionalGuestAmount MaxAdditionalGuests = "2" AgeQualifyingCode = "8" Amount = "20.00" CurrencyCode = "EUR"/>
                </AdditionalGuestAmounts>
                <MealsIncluded MealPlanCodes = "7"/>
              </Rate>
            </Rates>
            <Supplements>
              <Supplement Start = "2013-12-20" End = "2013-12-20" AgeQualifyingCode = "10" CurrencyCode = "EUR" Amount = "35.00" SupplementType = "Board" InvCode = "12"/>
              <Supplement Start = "2013-12-20" End = "2013-12-20" AgeQualifyingCode = "8" CurrencyCode = "EUR" Amount = "20.00" SupplementType = "Board" InvCode = "12"/>
            </Supplements>
            <SellableProducts>
              <SellableProduct InvCode = "JUN_1" InvType = "ROOM" InvStatusType = "Active"/>
            </SellableProducts>
            <Commission Percent = "15.00"/>
          </RatePlan>
          <RatePlan RatePlanType = "11" RatePlanCode = "LOWCOST" RatePlanStatusType = "Active">
            <Rates>
              <Rate Start = "2013-12-21" End = "2013-12-21">
                <BaseByGuestAmts>
                  <BaseByGuestAmt AmountAfterTax = "300.00" CurrencyCode = "EUR" NumberOfGuests = "3"/>
                </BaseByGuestAmts>
                <AdditionalGuestAmounts>
                  <AdditionalGuestAmount MaxAdditionalGuests = "1" AgeQualifyingCode = "8" Amount = "40.00" CurrencyCode = "EUR"/>
                  <AdditionalGuestAmount MaxAdditionalGuests = "2" AgeQualifyingCode = "8" Amount = "20.00" CurrencyCode = "EUR"/>
                </AdditionalGuestAmounts>
                <MealsIncluded MealPlanCodes = "7"/>
              </Rate>
            </Rates>
            <Supplements>
              <Supplement Start = "2013-12-21" End = "2013-12-21" AgeQualifyingCode = "10" CurrencyCode = "EUR" Amount = "35.00" SupplementType = "Board" InvCode = "12"/>
              <Supplement Start = "2013-12-21" End = "2013-12-21" AgeQualifyingCode = "8" CurrencyCode = "EUR" Amount = "20.00" SupplementType = "Board" InvCode = "12"/>
            </Supplements>
            <SellableProducts>
              <SellableProduct InvCode = "JUN_1" InvType = "ROOM" InvStatusType = "Active"/>
            </SellableProducts>
            <Commission Percent = "15.00"/>
          </RatePlan>
          <RatePlan RatePlanType = "11" RatePlanCode = "LOWCOST" RatePlanStatusType = "Deactivated">
            <Rates>
              <Rate Start = "2013-12-22" End = "2013-12-22">
                <BaseByGuestAmts>
                  <BaseByGuestAmt AmountAfterTax = "300.00" CurrencyCode = "EUR" NumberOfGuests = "3"/>
                </BaseByGuestAmts>
                <AdditionalGuestAmounts>
                  <AdditionalGuestAmount MaxAdditionalGuests = "1" AgeQualifyingCode = "8" Amount = "40.00" CurrencyCode = "EUR"/>
                  <AdditionalGuestAmount MaxAdditionalGuests = "2" AgeQualifyingCode = "8" Amount = "20.00" CurrencyCode = "EUR"/>
                </AdditionalGuestAmounts>
                <MealsIncluded MealPlanCodes = "7"/>
              </Rate>
            </Rates>
            <Supplements>
              <Supplement Start = "2013-12-22" End = "2013-12-22" AgeQualifyingCode = "10" CurrencyCode = "EUR" Amount = "35.00" SupplementType = "Board" InvCode = "12"/>
              <Supplement Start = "2013-12-22" End = "2013-12-22" AgeQualifyingCode = "8" CurrencyCode = "EUR" Amount = "20.00" SupplementType = "Board" InvCode = "12"/>
            </Supplements>
            <SellableProducts>
              <SellableProduct InvCode = "JUN_1" InvType = "ROOM" InvStatusType = "Active"/>
            </SellableProducts>
            <Commission Percent = "15.00"/>
          </RatePlan>
          <RatePlan RatePlanType = "11" RatePlanCode = "LOWCOST" RatePlanStatusType = "Deactivated">
            <Rates>
              <Rate Start = "2013-12-23" End = "2013-12-23">
                <BaseByGuestAmts>
                  <BaseByGuestAmt AmountAfterTax = "300.00" CurrencyCode = "EUR" NumberOfGuests = "3"/>
                </BaseByGuestAmts>
                <AdditionalGuestAmounts>
                  <AdditionalGuestAmount MaxAdditionalGuests = "1" AgeQualifyingCode = "8" Amount = "40.00" CurrencyCode = "EUR"/>
                  <AdditionalGuestAmount MaxAdditionalGuests = "2" AgeQualifyingCode = "8" Amount = "20.00" CurrencyCode = "EUR"/>
                </AdditionalGuestAmounts>
                <MealsIncluded MealPlanCodes = "7"/>
              </Rate>
            </Rates>
            <Supplements>
              <Supplement Start = "2013-12-23" End = "2013-12-23" AgeQualifyingCode = "10" CurrencyCode = "EUR" Amount = "35.00" SupplementType = "Board" InvCode = "12"/>
              <Supplement Start = "2013-12-23" End = "2013-12-23" AgeQualifyingCode = "8" CurrencyCode = "EUR" Amount = "20.00" SupplementType = "Board" InvCode = "12"/>
            </Supplements>
            <SellableProducts>
              <SellableProduct InvCode = "JUN_1" InvType = "ROOM" InvStatusType = "Active"/>
            </SellableProducts>
            <Commission Percent = "15.00"/>
          </RatePlan>
          <RatePlan RatePlanType = "11" RatePlanCode = "LOWCOST" RatePlanStatusType = "Deactivated">
            <Rates>
              <Rate Start = "2013-12-24" End = "2013-12-24">
                <BaseByGuestAmts>
                  <BaseByGuestAmt AmountAfterTax = "300.00" CurrencyCode = "EUR" Type = "25"/>
                </BaseByGuestAmts>
                <AdditionalGuestAmounts>
                  <AdditionalGuestAmount MaxAdditionalGuests = "1" AgeQualifyingCode = "8" Amount = "40.00" CurrencyCode = "EUR"/>
                  <AdditionalGuestAmount MaxAdditionalGuests = "2" AgeQualifyingCode = "8" Amount = "20.00" CurrencyCode = "EUR"/>
                </AdditionalGuestAmounts>
                <MealsIncluded MealPlanCodes = "7"/>
              </Rate>
            </Rates>
            <Supplements>
              <Supplement Start = "2013-12-24" End = "2013-12-24" AgeQualifyingCode = "10" CurrencyCode = "EUR" Amount = "35.00" SupplementType = "Board" InvCode = "12"/>
              <Supplement Start = "2013-12-24" End = "2013-12-24" AgeQualifyingCode = "8" CurrencyCode = "EUR" Amount = "20.00" SupplementType = "Board" InvCode = "12"/>
            </Supplements>
            <SellableProducts>
              <SellableProduct InvCode = "JUN_1" InvType = "ROOM" InvStatusType = "Active"/>
            </SellableProducts>
            <Commission Percent = "15.00"/>
          </RatePlan>
          <RatePlan RatePlanType = "11" RatePlanCode = "LOWCOST" RatePlanStatusType = "Deactivated">
            <Rates>
              <Rate Start = "2013-12-25" End = "2013-12-25">
                <BaseByGuestAmts>
                  <BaseByGuestAmt AmountAfterTax = "300.00" CurrencyCode = "EUR" Type = "25"/>
                </BaseByGuestAmts>
                <AdditionalGuestAmounts>
                  <AdditionalGuestAmount MaxAdditionalGuests = "1" AgeQualifyingCode = "8" Amount = "40.00" CurrencyCode = "EUR"/>
                  <AdditionalGuestAmount MaxAdditionalGuests = "2" AgeQualifyingCode = "8" Amount = "20.00" CurrencyCode = "EUR"/>
                </AdditionalGuestAmounts>
                <MealsIncluded MealPlanCodes = "7"/>
              </Rate>
            </Rates>
            <Supplements>
              <Supplement Start = "2013-12-25" End = "2013-12-25" AgeQualifyingCode = "10" CurrencyCode = "EUR" Amount = "35.00" SupplementType = "Board" InvCode = "12"/>
              <Supplement Start = "2013-12-25" End = "2013-12-25" AgeQualifyingCode = "8" CurrencyCode = "EUR" Amount = "20.00" SupplementType = "Board" InvCode = "12"/>
            </Supplements>
            <SellableProducts>
              <SellableProduct InvCode = "JUN_1" InvType = "ROOM" InvStatusType = "Active"/>
            </SellableProducts>
            <Commission Percent = "15.00"/>
          </RatePlan>
          <RatePlan RatePlanType = "11" RatePlanCode = "LOWCOST" RatePlanStatusType = "Deactivated">
            <Rates>
              <Rate Start = "2013-12-25" End = "2013-12-25">
                <BaseByGuestAmts>
                  <BaseByGuestAmt AmountAfterTax = "300.00" CurrencyCode = "EUR" Type = "14" Code = "2-0-0"/>
                  <BaseByGuestAmt AmountAfterTax = "330.00" CurrencyCode = "EUR" Type = "14" Code = "2-1-0"/>
                </BaseByGuestAmts>
                <MealsIncluded MealPlanCodes = "7"/>
              </Rate>
            </Rates>
            <Supplements>
              <Supplement Start = "2013-12-25" End = "2013-12-25" CurrencyCode = "EUR" Amount = "35.00" SupplementType = "Board" InvCode = "12" ChargeTypeCode = "2-0-0"/>
              <Supplement Start = "2013-12-25" End = "2013-12-25" CurrencyCode = "EUR" Amount = "20.00" SupplementType = "Board" InvCode = "12" ChargeTypeCode = "3-0-0"/>
            </Supplements>
            <SellableProducts>
              <SellableProduct InvCode = "JUN_1" InvType = "ROOM" InvStatusType = "Active"/>
            </SellableProducts>
            <Commission Percent = "15.00"/>
          </RatePlan>
        </RatePlans>
      </HotelRatePlanRetrieveResult>
    </HotelRatePlanRetrieveResponse>

Gets the Rate BAR for the Hotel 12 from 2013-12-20 to 2013-12-25. In
this case, the rate LOWCOST has two rooms associated, you will receive a
RatePlan for each day-room-rate.

|

**Example for Derived RatePlan**

:

    <HotelRatePlanRetrieveResponse xmlns = "http://schemas.xmltravelgate.com/hubpush/provider/2012/10">
      <HotelRatePlanRetrieveResult Version = "0">
        <RatePlans HotelCode = "1" xmlns = "http://www.opentravel.org/OTA/2003/05">
          <RatePlan RatePlanCode = "DRV" BaseRatePlanCode = "SRATE" AdjustedPercentage = "10.00" AdjustUpIndicator = "false" RatePlanStatusType = "Active">
            <Rates>
              <Rate Start = "2014-07-01" End = "2014-07-01"/>
            </Rates>
            <Description>
              <Text>TarifaDerivada</Text>
            </Description>
          </RatePlan>
          <RatePlan RatePlanCode = "DRV" BaseRatePlanCode = "SRATE" AdjustedPercentage = "10.00" AdjustUpIndicator = "false" RatePlanStatusType = "Active">
            <Rates>
              <Rate Start = "2014-07-02" End = "2014-07-02"/>
            </Rates>
            <Description>
              <Text>TarifaDerivada</Text>
            </Description>
          </RatePlan>
          <RatePlan RatePlanCode = "DRV" BaseRatePlanCode = "SRATE" AdjustedPercentage = "10.00" AdjustUpIndicator = "false" RatePlanStatusType = "Deactivated">
            <Rates>
              <Rate Start = "2014-07-03" End = "2014-07-03"/>
            </Rates>
            <Description>
              <Text>TarifaDerivada</Text>
            </Description>
          </RatePlan>
          <RatePlan RatePlanCode = "DRV" BaseRatePlanCode = "SRATE" AdjustedPercentage = "10.00" AdjustUpIndicator = "false" RatePlanStatusType = "Deactivated">
            <Rates>
              <Rate Start = "2014-07-04" End = "2014-07-04"/>
            </Rates>
            <Description>
              <Text>TarifaDerivada</Text>
            </Description>
          </RatePlan>
          <RatePlan RatePlanCode = "DRV" BaseRatePlanCode = "SRATE" AdjustedPercentage = "10.00" AdjustUpIndicator = "false" RatePlanStatusType = "Deactivated">
            <Rates>
              <Rate Start = "2014-07-05" End = "2014-07-05"/>
            </Rates>
            <Description>
              <Text>TarifaDerivada</Text>
            </Description>
          </RatePlan>
        </RatePlans>
      </HotelRatePlanRetrieveResult>
    </HotelRatePlanRetrieveResponse>

For a derived rate you will not receive the rooms associated. Derived
rates have associated all the rooms from the base rate plan.

  ------------------------------------------------------------------------
  Element      N T Description
               u y 
               m p 
               b e 
               e   
               r   
  ------------ - - -------------------------------------------------------
  HotelRatePla 1   Root Node
  nRetrieveRes     
  ponse/HotelR     
  atePlanRetri     
  eveResult        

  Success      0   Should only be present if it was a successful response.
               .   The Errors node should not be present if the Success
               .   node is present.
               1   

  RatePlans    0   Present when sucess
               .   
               .   
               1   

  <*@HotelCode 1 S Hotel code whose information is provided by the method
  >\*            t 
                 r 
                 i 
                 n 
                 g 

  RatePlans/Ra 0   Present if rate exists
  tePlan       .   
               .   
               1   

  <*@RatePlanT 0 I OTA RPT Code (11 - Package)
  ype>\*       . n 
               . t 
               1 e 
                 g 
                 e 
                 r 

  <*@RatePlanC 1 S Rate code
  ode>\*         t 
                 r 
                 i 
                 n 
                 g 

  <*@RatePlanS 1 S Active or Deactivated
  tatusType>\*   t 
                 r 
                 i 
                 n 
                 g 

  <*@BaseRateP 0 S Rate code of the base RatePlan. Only used for derived
  lanCode>\*   . t rates
               . r 
               1 i 
                 n 
                 g 

  <*@AdjustedP 0 D The percentage off the base rate plan amount used to
  ercentage>\* . e determine the price of this derived rate plan. Only
               . c used for derived rates
               1 i 
                 m 
                 a 
                 l 

  <*@AdjustedA 0 D The amount which should be added to the base rate plan
  mount>\*     . e to determine the price of this derived rate plan. Only
               . c used for derived rates
               1 i 
                 m 
                 a 
                 l 

  <*@AdjustUpI 0 B When true, the adjusted amount or adjusted percentage
  ndicator>\*  . o is added to the amount specified for the base rate plan
               . o to determine the derived rate amount. When false, the
               1 l adjusted amount or adjusted percentage is subtracted
                 e from the amount specified for the base rate plan to
                 a determine the derived rate amount. Only used for
                 n derived rates

  RatePlans/Ra 1   
  tePlan/Rates     
  /Rate            

  <*@Start>\*  1 D Start date of rate
                 a 
                 t 
                 e 

  <*@End>\*    1 D Start date of rate
                 a 
                 t 
                 e 

  RatePlans/Ra 0   Not used for derived rates
  tePlan/Rates .   
  /Rate/BaseBy .   
  GuestAmts    1   

  RatePlans/Ra 1   
  tePlan/Rates .   
  /Rate/BaseBy .   
  GuestAmts/Ba n   
  seByGuestAmt     

  <*@AmountAft 1 D Total amount for @NumberOfGuests by day indicated
  erTax>\*       e 
                 c 
                 i 
                 m 
                 a 
                 l 

  <*@NumberOfG 0 I How many adults are the @AmountAfterTax for day
  uests>\*     . n indicated. If @NumberOfGuests is not informed then
               . t @Type must be informed
               1 e 
                 g 
                 e 
                 r 

  <*@Type>\*   0 I Amounts are per Room or per Occupancy instead of per
               . n Pax. If @Type=25, price is per room, 1 BaseByGuestAmt
               . t is returned and @NumberOfGuests and
               1 e AdditionalGuestAmounts are not returned. If @Type=14,
                 g price is per occupancy, @Code is returned and
                 e @NumberOfGuests and AdditionalGuestAmounts are not
                 r returned.

  <*@Code>\*   0 S Returned if @Type=14. The occupancy code is defined by
               . t AdultNumber-ChildNumber-InfantNumber. @Code for an
               . r occupancy of 2 adults, 1 child and 0 babies would be
               1 i "2-1-0".
                 n 
                 g 

  <*@CurrencyC 1 S ISO Currency (EUR)
  ode>\*         t 
                 r 
                 i 
                 n 
                 g 

  RatePlans/Ra 0   
  tePlan/Rates .   
  /Rate/Additi .   
  onalGuestAmo 1   
  unts             

  RatePlans/Ra 1   
  tePlan/Rates .   
  /Rate/Additi .   
  onalGuestAmo n   
  unts/Additio     
  nalGuestAmou     
  nt               

  <*@MaxAdditi 1 I Indicates the number of guest to apply additional
  onalGuests>\   n price, not is the max of guests, for example, if its 2,
  *              t is for the second pax not to 2 paxes.
                 e 
                 g 
                 e 
                 r 

  <*@Type>\*   0 S OTA AmountDeterminationType. If not specified then the
               . t price is a suplement, if @Type is Exclusive then the
               . r the price is absolute.
               1 i 
                 n 
                 g 

  <*@AgeQualif 1 I (10 - Adult,8 - Child,7 - Infant)
  yingCode>\*    n 
                 t 
                 e 
                 g 
                 e 
                 r 

  <*@Amount>\* 1 D Price for each additional pax
                 e 
                 c 
                 i 
                 m 
                 a 
                 l 

  <*@CurrencyC 1 S ISO Currency (EUR)
  ode>\*         t 
                 r 
                 i 
                 n 
                 g 

  RatePlans/Ra 0   Present if meal included
  tePlan/Rates .   
  /Rate/MealsI .   
  ncluded      1   

  <*@MealPlanC 1 I OTA MPT Code
  odes>\*        n 
                 t 
                 e 
                 g 
                 e 
                 r 

  RatePlans/Ra 0   Present if supplements by board exists
  tePlan/Suppl .   
  ements       .   
               1   

  RatePlans/Ra 1   
  tePlan/Suppl .   
  ements/Suppl .   
  ement        n   

  <*@Start>\*  1 D Start date of this supplement
                 a 
                 t 
                 e 

  <*@End>\*    1 D End date of this supplement
                 a 
                 t 
                 e 

  <*@AgeQualif 0 I Age qualifyingCode which affects this supplement (10 -
  yingCode>\*  . n Adult,8 - Child,7 - Infant). Not returned if charging
               . t board supplement by occupancy.
               1 e 
                 g 
                 e 
                 r 

  <*@ChargeTyp 0 S Indicates the board supplement occupancy. Only returned
  eCode>\*     . t if charging board supplement by occupancy. The
               . r occupancy code is defined by
               1 i AdultNumber-ChildNumber-InfantNumber. @ChargeTypeCode
                 n for an occupancy of 2 adults, 1 child and 0 babies
                 g would be "2-1-0".

  <*@CurrencyC 1 S ISO Currency (EUR)
  ode>\*         t 
                 r 
                 i 
                 n 
                 g 

  <*@Amount>\* 1 D Amount of supplement
                 e 
                 c 
                 i 
                 m 
                 a 
                 l 

  <*@Supplemen 1 S (Board)
  tType>\*       t 
                 r 
                 i 
                 n 
                 g 

  <*@InvCode>\ 1 S OTA MPT Code if @SupplementType is Board
  *              t 
                 r 
                 i 
                 n 
                 g 

  RatePlans/Ra 0   List of sellable products. Null for derived rates.
  tePlan/Sella .   
  bleProducts  .   
               1   

  RatePlans/Ra 1   
  tePlan/Sella .   
  bleProducts/ .   
  SellableProd n   
  uct              

  <*@InvCode>\ 1 I Sellable Product Code
  *              n 
                 t 
                 e 
                 g 
                 e 
                 r 

  <*@InvType>\ 1 I Sellable product type (ROOM)
  *              n 
                 t 
                 e 
                 g 
                 e 
                 r 

  <*@InvStatus 1 S Active or Deactivated
  Type>\*        t 
                 r 
                 i 
                 n 
                 g 

  RatePlans/Ra 1 S Rate description
  tePlan/Descr   t 
  iption/Text    r 
                 i 
                 n 
                 g 
  ------------------------------------------------------------------------

|

HotelAvailRetrieve
==================

Providers will send an HotelAvailRetrieveRQ message to retrieve a
complete break down of availability. XTG will return break down of hotel
/ rates / rooms.

|

HotelAvailRetrieveRQ
====================

:

    <HotelAvailRetrieve>
      <request>
        <POS>
          <Source>
            <RequestorID ID = "Provider1"></RequestorID>
            <BookingChannel>
              <CompanyName Code = "ClientTravelAgency1"/>
            </BookingChannel>
            <TPA_Extensions>
              <Param key = "onlyActive" value = "0"/>
            </TPA_Extensions>
          </Source>
        </POS>
        <HotelAvailRequests>
          <HotelAvailRequest>
            <DateRange Start = "2013-12-20" End = "2013-12-25"/>
            <HotelRef HotelCode = "12"/>
            <RatePlanCandidates>
              <RatePlanCandidate RatePlanCode = "BAR"></RatePlanCandidate>
            </RatePlanCandidates>
          </HotelAvailRequest>
        </HotelAvailRequests>
      </request>
    </HotelAvailRetrieve>

+-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Element | Number | Type | Description
| +===================================================================+==========+==========+====================================================================================================================================================================+
| POS/Source/TPA\_Extensions | 0..1 | | Optional, empty only active
RatePlans/Rooms will be recieved.
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Param | 1 | |
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| <*@key>\* | 1 | String | onlyActive
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| <*@value>\* | 1 | String | 1 - You will recieve all active
RatePlans/Rooms data. 0 - Active and deactivated RatePlans/Rooms will be
recieved. (Same case than wihout TPA\_Extensions node.)
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| HotelAvailRetrieve/request/HotelAvailRequests/HotelAvailRequest | 1 |
| Root Node
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| DateRange | 1 | | Contains date filter
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| <*@Start>\* | 1 | Date | Start date to search rates
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| <*@End>\* | 1 | Date | End date to search rates
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| HotelRef | 1 | | Contains hotel filter
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| <*@HotelCode>\* | 1 | String | Hotel date to search rates
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| RatePlanCandidates | 0..1 | | If exists, contains rate filter
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| RatePlanCandidates/RatePlanCandidate | 1..n | |
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| <*@RatePlanCode>\* | 1 | String | Rate Plan Code to search rates
| +-------------------------------------------------------------------+----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|

HotelAvailRetrieveRS
====================

**Example for RatePlan**

:

    <HotelAvailRetrieveResponse>
      <HotelAvailRetrieveResult>
        <Success/>
        <AvailStatusMessages HotelCode = "12">
          <AvailStatusMessage BookingLimit = "9" BookingSold = "0">
            <StatusApplicationControl Start = "2013-12-20" End = "2013-12-25" RatePlanCode = "BAR" InvCode = "APT" InvType = "ROOM" Mon = "true" Tue = "true" Weds = "true" Thur = "false" Fri = "true" Sat = "true" Sun = "true"/>
            <LengthsOfStay ArrivalDateBased = "true">
              <LengthOfStay Time = "2" TimeUnit = "Day" MinMaxMessageType = "MinLOS"/>
              <LengthOfStay Time = "8" TimeUnit = "Day" MinMaxMessageType = "MaxLOS"/>
            </LengthsOfStay>
            <RestrictionStatus Status = "Open" SellThroughOpenIndicator = "false" MinAdvancedBookingOffset = "5"/>
          </AvailStatusMessage>
          <AvailStatusMessage BookingLimit = "12" BookingSold = "2">
            <StatusApplicationControl Start = "2013-12-20" End = "2013-12-21" RatePlanCode = "LOWCOST" InvCode = "JUN_1" InvType = "ROOM" Mon = "false" Tue = "false" Weds = "false" Thur = "false" Fri = "true" Sat = "true" Sun = "false"/>
            <RestrictionStatus Restriction = "Master" Status = "Close"/>
          </AvailStatusMessage>
          <AvailStatusMessage BookingLimit = "12" BookingSold = "2">
            <StatusApplicationControl Start = "2013-12-22" End = "2013-12-25" RatePlanCode = "LOWCOST" InvCode = "JUN_1" InvType = "ROOM" Mon = "true" Tue = "true" Weds = "true" Thur = "false" Fri = "false" Sat = "false" Sun = "true"/>
            <LengthsOfStay ArrivalDateBased = "true">
              <LengthOfStay Time = "3" TimeUnit = "Day" MinMaxMessageType = "MinLOS"/>
              <LengthOfStay Time = "9" TimeUnit = "Day" MinMaxMessageType = "MaxLOS"/>
            </LengthsOfStay>
            <RestrictionStatus Status = "Close" Restriction = "Arrival"/>
          </AvailStatusMessage>
          <AvailStatusMessage BookingLimit = "12" BookingSold = "2">
            <StatusApplicationControl Start = "2013-12-20" End = "2013-12-25" RatePlanCode = "LOWCOST" InvCode = "STD1" InvType = "ROOM" Mon = "true" Tue = "true" Weds = "true" Thur = "false" Fri = "true" Sat = "true" Sun = "true"/>
            <LengthsOfStay ArrivalDateBased = "false">
              <LengthOfStay Time = "1" TimeUnit = "Day" MinMaxMessageType = "MinLOS"/>
              <LengthOfStay Time = "2" TimeUnit = "Day" MinMaxMessageType = "MaxLOS"/>
            </LengthsOfStay>
            <RestrictionStatus Status = "Open" SellThroughOpenIndicator = "false" MinAdvancedBookingOffset = "6" MaxAdvancedBookingOffset = "999"/>
          </AvailStatusMessage>
          <AvailStatusMessage>
            <StatusApplicationControl Start = "2013-12-26" End = "2013-12-27" RatePlanCode = "LOWCOST" InvCode = "STD1" InvType = "ROOM" Mon = "true" Tue = "true" Weds = "true" Thur = "false" Fri = "true" Sat = "true" Sun = "true"/>
            <RestrictionStatus Status = "Open" SellThroughOpenIndicator = "false" MaxAdvancedBookingOffset = "2"/>
          </AvailStatusMessage>
        </AvailStatusMessages>
      </HotelAvailRetrieveResult>
    </HotelAvailRetrieveResponse>

**Example for Derived RatePlan**

:

    <HotelAvailRetrieveResponse xmlns = "http://schemas.xmltravelgate.com/hubpush/provider/2012/10">
      <HotelAvailRetrieveResult Version = "0">
        <Success xmlns = "http://www.opentravel.org/OTA/2003/05"/>
        <AvailStatusMessages HotelCode = "1" xmlns = "http://www.opentravel.org/OTA/2003/05">
          <AvailStatusMessage>
            <StatusApplicationControl Start = "2014-07-01" End = "2014-07-31" RatePlanCode = "DRV" Mon = "true" Tue = "true" Weds = "true" Thur = "true" Fri = "true" Sat = "true" Sun = "true"/>
            <LengthsOfStay ArrivalDateBased = "false">
              <LengthOfStay Time = "3" TimeUnit = "Day" MinMaxMessageType = "MinLOS"/>
              <LengthOfStay Time = "3" TimeUnit = "Day" MinMaxMessageType = "MaxLOS"/>
            </LengthsOfStay>
            <RestrictionStatus MinAdvancedBookingOffset = "5"/>
          </AvailStatusMessage>
        </AvailStatusMessages>
      </HotelAvailRetrieveResult>
    </HotelAvailRetrieveResponse>

  -------------------------------------------------------------------------
  Element     N Ty Description
              u pe 
              m    
              b    
              e    
              r    
  ----------- - -- --------------------------------------------------------
  HotelAvailR 1    Root Node
  etrieveResp      
  onse/HotelA      
  vailRetriev      
  eResult          

  Success     0    Should only be present if it was a successful response.
              .    The Errors node should not be present if the Success
              .    node is present.
              1    

  AvailStatus 0    Present when success
  Messages    .    
              .    
              1    

  <*@HotelCod 1 St Hotel code whose information is provided by the method
  e>\*          ri 
                ng 

  AvailStatus 0    
  Messages/Av .    
  ailStatusMe .    
  ssage       n    

  <*@BookingL 0 In Identifies the number of available rooms per Room &
  imit>\*     . te RatePlan for the indicated dates. Not mandatory when the
              . ge @Status is Close or is a derived rate
              1 r  

  <*@BookingS 0 In Identifies the number of sold rooms per Room & RatePlan
  old>\*      . te for the indicated dates. This value is reset when a new
              . ge BookingLimit is charged by an HotelAvailNotif request.
              1 r  Not mandatory when the @Status is Close or is a derived
                   rate

  AvailStatus 1    
  Messages/Av      
  ailStatusMe      
  ssage/Statu      
  sApplicatio      
  nControl         

  <*@Start>\* 1 Da Start date
                te 

  <*@End>\*   1 Da End date
                te 

  <*@RatePlan 1 St Rate Plan Code
  Code>\*       ri 
                ng 

  <*@InvCode> 0 St Room Code. Null for derived rates
  \*          . ri 
              . ng 
              1    

  <*@InvType> 0 St Product type (ROOM). Null for derived rates
  \*          . ri 
              . ng 
              1    

  <*@Mon>\*   1 Bo Indicates whether the AvailStatusMessage data applies to
                ol Mondays
                ea 
                n  

  <*@Tue>\*   1 Bo Indicates whether the AvailStatusMessage data applies to
                ol Tuesdays
                ea 
                n  

  <*@Weds>\*  1 Bo Indicates whether the AvailStatusMessage data applies to
                ol Wednesdays
                ea 
                n  

  <*@Thur>\*  1 Bo Indicates whether the AvailStatusMessage data applies to
                ol Thursdays
                ea 
                n  

  <*@Fri>\*   1 Bo Indicates whether the AvailStatusMessage data applies to
                ol Fridays
                ea 
                n  

  <*@Sat>\*   1 Bo Indicates whether the AvailStatusMessage data applies to
                ol Saturdays
                ea 
                n  

  <*@Sun>\*   1 Bo Indicates whether the AvailStatusMessage data applies to
                ol Sundays
                ea 
                n  

  AvailStatus 0    
  Messages/Av .    
  ailStatusMe .    
  ssage/Lengt 1    
  hsOfStay         

  <*@ArrivalD 0 Bo When its true, the minimum and maximum stay is checked
  ateBased>\* . ol ONLY the first day of the availability, when false or
              . ea not indicated, the minimum and maximum stay is checked
              1 n  all the availability days.

  AvailStatus 1    
  Messages/Av .    
  ailStatusMe .    
  ssage/Lengt 2    
  hsOfStay/Le      
  ngthOfStay       

  <*@Time>\*  1 In Indicates the number of @TimeUnit for this stay
                te 
                ge 
                r  

  <*@TimeUnit 1 St Day
  >\*           ri 
                ng 

  <*@MinMaxMe 1 St (MinLOS, MaxLOS) Indicates the minimum or maximum stay
  ssageType>\   ri for his AvailStatusMessage.
  *             ng 

  AvailStatus 0    
  Messages/Av .    
  ailStatusMe .    
  ssage/Restr 1    
  ictionStatu      
  s                

  <*@Status>\ 1 St (Open, Close)
  *             ri 
                ng 

  <*@Restrict 0 St Master. This is the master availability. If master
  ion>\*      . ri availability is ‘Closed’, the product is not bookable if
              . ng any of the stay dates includes one of the dates
              1    specified by the Application Control element. If master
                   availability is ‘Open’, additional restrictions on
                   arrival and departure may be placed (Master, Arrival,
                   Departure)

  <*@MinAdvan 0 In Minimum number of days before the check-in date after
  cedBookingO . te which the product is not available to be booked. This
  ffset>\*    . ge restriction is usually used to offer discounts on early
              1 r  bookings

  <*@MaxAdvan 0 In Maximum number of days before the check-in date after
  cedBookingO . te which the product is not available to be booked. This
  ffset>\*    . ge restriction is usually used to offer last minute
              1 r  discounts on unsold inventory.

  <*@SellThro 0 Bo When @Status is open, in this element you can indicate
  ughOpenIndi . ol this room or room/ratePlan can be sold without limit
  cator>\*    . ea (like BookingLimit=MaxInteger). Null for derived rates
              1 n  
  -------------------------------------------------------------------------

|

HotelResRetrieve
================

Providers will send an HotelResRetrieveRQ message to retrieve a list of
seller reservations.

|

HotelResRetrieveRQ
==================

:

    <HotelResRetrieve>
      <request>
        <POS>
          <Source>
            <RequestorID ID = "Provider1"/>
            <BookingChannel>
              <CompanyName Code = "ClientTravelAgency1"/>
            </BookingChannel>
          </Source>
        </POS>
        <UniqueID ID = "123456" ID_Context = "Client"/> 
        <ReadRequests>
          <HotelReadRequest HotelCode="1608">
            <SelectionCriteria Start="2013-11-25" End="2013-11-28" DateType="DepartureDate"/>
          </HotelReadRequest>
          <HotelReadRequest>
            <SelectionCriteria Start = "2015-12-23" End = "2015-12-28" DateType = "ArrivalDate"/> 
          </HotelReadRequest>
        </ReadRequests>
      </request>
    </HotelResRetrieve>

  -------------------------------------------------------------------------
  Element           Numbe Type  Description
                    r           
  ----------------- ----- ----- -------------------------------------------
  HotelResRetrieve/ 1           Root Node
  request                       

  UniqueID          0..1        If present filter by UniqueID content

  <*@ID>\*          1     Strin Booking ID
                          g     

  <*@IDContext>\*   1     Strin (Client, Provider, Internal)
                          g     

  ReadRequests      0..1        If present filter by its content

  ReadRequests/Hote 1..n        Node containing the read request data.
  lReadRequest                  

  <*@HotelCode>\*   0..1  Strin Hotel code.
                          g     

  HotelReadRequest/ 1           
  SelectionCriteria             

  <*@Start>\*       1     DateT Start date to search bookings. DateTime
                          ime   Format is yyyy-MM-ddThh:mm:ss Date must be
                                in UTC

  <*@End>\*         1     DateT End date to search bookings. DateTime
                          ime   Format is yyyy-MM-ddThh:mm:ss Date must be
                                in UTC

  <*@DateType>\*    1     Strin (ArrivalDate, CreateDate, DepartureDate,
                          g     LastUpdateDate)
  -------------------------------------------------------------------------

|

HotelResRetrieveRS
==================

:

    <HotelResRetrieveResponse xmlns = "http://schemas.xmltravelgate.com/hubpush/client/2012/10">
      <HotelResRetrieveResult Version = "0">
        <Success xmlns = "http://www.opentravel.org/OTA/2003/05"/>
        <HotelReservations xmlns = "http://www.opentravel.org/OTA/2003/05">
          <HotelReservation ResStatus = "Confirmed" CreateDateTime = "2013-09-01T11:09:57.5387811Z">
            <RoomStays>
              <RoomStay>
                <RoomTypes>
                  <RoomType RoomTypeCode = "STD1" RoomID = "1">
                    <RoomDescription>
                      <Text>Standard</Text>
                    </RoomDescription>
                  </RoomType>
                </RoomTypes>
                <RatePlans>
                  <RatePlan RatePlanCode = "BAR">
                    <RatePlanDescription>
                      <Text>Best Available Rate</Text>
                    </RatePlanDescription>
                    <Commission Percent = "15.00"/>
                  </RatePlan>
                </RatePlans>
                <RoomRates>
                  <RoomRate EffectiveDate = "2013-09-03" ExpireDate = "2013-09-07" RoomTypeCode = "STD1" InvBlockCode = "7" RatePlanCode = "BAR">
                    <Rates>
                      <Rate EffectiveDate = "2013-09-03" ExpireDate = "2013-09-07">
                        <Base AmountBeforeTax = "200.00" AmountAfterTax = "200.00" CurrencyCode = "EUR"/>
                        <CancelPolicies>
                          <CancelPenalty PolicyCode = "0912f3bc-40cc-4566-a5d7-0d2833ab62de"/>
                          <CancelPenalty PolicyCode = "cd4aa15e-82e4-420a-937e-63e802ba352a"/>
                        </CancelPolicies>
                      </Rate>
                    </Rates>
                    <Total AmountBeforeTax = "200.00" AmountAfterTax = "200.00" CurrencyCode = "EUR"/>
                  </RoomRate>
                </RoomRates>
                <CancelPenalties>
                  <CancelPenalty PolicyCode = "0912f3bc-40cc-4566-a5d7-0d2833ab62de" NonRefundable = "false">
                    <Deadline AbsoluteDeadline = "2013-08-29" OffsetTimeUnit = "Day" OffsetUnitMultiplier = "5" OffsetDropTime = "BeforeArrival"/>
                    <AmountPercent Percent = "15.00" CurrencyCode = "EUR"/>
                  </CancelPenalty>
                  <CancelPenalty PolicyCode = "cd4aa15e-82e4-420a-937e-63e802ba352a" NonRefundable = "false">
                    <Deadline AbsoluteDeadline = "2013-08-31" OffsetTimeUnit = "Day" OffsetUnitMultiplier = "3" OffsetDropTime = "BeforeArrival"/>
                    <AmountPercent NmbrOfNights = "2" CurrencyCode = "EUR"/>
                  </CancelPenalty>
                </CancelPenalties>
                <BasicPropertyInfo HotelCode = "12" HotelName = "Adagio City Aparthotel Annecy Centre"/>
                <ServiceRPHs>
                  <ServiceRPH RPH = "1"/>
                  <ServiceRPH RPH = "2"/>
                </ServiceRPHs>
              </RoomStay>
            </RoomStays>
            <ResGuests>
              <ResGuest ResGuestRPH = "1" AgeQualifyingCode = "10">
                <Profiles>
                  <ProfileInfo>
                    <Profile>
                      <Customer>
                        <PersonName>
                          <NamePrefix>Mr</NamePrefix>
                          <GivenName>Test11</GivenName>
                          <Surname>TestAp11</Surname>
                        </PersonName>
                      </Customer>
                    </Profile>
                  </ProfileInfo>
                </Profiles>
                <GuestCounts>
                  <GuestCount Age = "30"/>
                </GuestCounts>
              </ResGuest>
              <ResGuest ResGuestRPH = "2" AgeQualifyingCode = "10">
                <Profiles>
                  <ProfileInfo>
                    <Profile>
                      <Customer>
                        <PersonName>
                          <NamePrefix>Mr</NamePrefix>
                          <GivenName>Test22</GivenName>
                          <Surname>TestAp22</Surname>
                        </PersonName>
                      </Customer>
                    </Profile>
                  </ProfileInfo>
                </Profiles>
                <GuestCounts>
                  <GuestCount Age = "30"/>
                </GuestCounts>
              </ResGuest>
            </ResGuests>
            <ResGlobalInfo>
              <Total AmountBeforeTax = "500.00" AmountAfterTax = "500.00" CurrencyCode = "USD"/>
              <Guarantee PaymentCode = "MerchantPayment"/>
              <HotelReservationIDs>
                <HotelReservationID ResID_Value = "123456" ResID_SourceContext = "Client"/>
                <HotelReservationID ResID_Value = "124" ResID_SourceContext = "Internal"/>
                <HotelReservationID ResID_Value = "115137" ResID_SourceContext = "Provider"/>
              </HotelReservationIDs>
              <Profiles>
                <ProfileInfo>
                  <Profile>
                    <Customer>
                      <PersonName>
                        <NamePrefix>Mr</NamePrefix>
                        <GivenName>Test12</GivenName>
                        <Surname>TestAp12</Surname>
                      </PersonName>
                      <Telephone PhoneTechType = "1" PhoneNumber = "1212121212" FormattedInd = "false" DefaultInd = "true"/>
                      <Email DefaultInd = "true" EmailType = "1">test@yourdomain.com</Email>
                      <Address Type = "1">
                        <AddressLine>B-15, Sector-57</AddressLine>
                        <CityName>NOIDA</CityName>
                        <PostalCode>201301</PostalCode>
                        <StateProv StateCode = "UP">Uttar Pradesh</StateProv>
                        <CountryName Code = "IN">INDIA</CountryName>
                      </Address>
                    </Customer>
                  </Profile>
                </ProfileInfo>
              </Profiles>
            </ResGlobalInfo>
          </HotelReservation>
        </HotelReservations>
      </HotelResRetrieveResult>
    </HotelResRetrieveResponse>

  ------------------------------------------------------------------------
  Element       Nu Typ Description
                mb e   
                er     
  ------------- -- --- ---------------------------------------------------
  HotelResRetri 1      Root Node
  eveResponse          

  HotelResRetri 1      Contains the result of reservation retrieve.
  eveResponse/H        
  otelResRetrie        
  veResult             

  HotelResRetri 0.     Should only be present if it was a successful
  eveResult/Suc .1     response. The Errors node should not be present if
  cess                 the Success node is present.

  HotelResRetri 0.     Node containing the reservation.
  eveResult/Hot .1     
  elReservation        
  s                    

  HotelReservat 1      Node containing information about the reservation.
  ions/HotelRes        
  ervation             

  <*@ResStatus> 1  Str Status of the reservation. Possible status are:
  \*               ing 'Confirmed', 'Requested' and 'Cancelled'

  <*@CreateDate 1  Dat Date and time when the reservation was made.
  Time>\*          eTi 
                   me  

  <*@LastModify 0. Dat Date and time when the reservation was modified.
  DateTime>\*   .1 eTi Should only be present if the reservation status is
                   me  'Cancelled'.

  HotelReservat 1      Node containing the RoomStays of the reservation.
  ion/RoomStays        

  RoomStays/Roo 1.     Node containing RoomStay information.
  mStay         .n     

  RoomStay/Room 1      Node containing information about rooms.
  Types                

  RoomTypes/Roo 1      Node containing information about one room.
  mType                

  <*@RoomTypeCo 1  Str Room code.
  de>\*            ing 

  <*@RoomID>\*  1  Str Id of the room.
                   ing 

  RoomType/Room 1      Node containing the description of the room.
  Description          

  RoomDescripti 1  Str Description of the room.
  on/Text          ing 

  RoomStay/Rate 1      Node containing information about RatePlans.
  Plans                

  RatePlans/Rat 1      Node containing information about one RatePlan.
  ePlan                

  <*@RatePlanCo 1      RatePlan code.
  de>\*                

  RatePlan/Rate 1      Node containing information the RatePlan
  PlanDescripti        description one RatePlan.
  on                   

  RatePlanDescr 1  Str Description of the RatePlan.
  iption/Text      ing 

  RatePlan/Comm 1      Node containing the commission of the RatePlan.
  ission               

  Percent       1  Dec Commission of the RatePlane.
                   ima 
                   l   

  RoomStay/Room 1      Node containing information about RoomRates.
  Rates                

  RoomRates/Roo 1      Node containing information about one RoomRate.
  mRate                

  <*@EffectiveD 1  Dat Effective date when the RoomRate start applying.
  ate>\*           e   

  <*@ExpireDate 1  Dat Expire date when the RoomRate ends applying. Check
  >\*              e   out night minus 1.

  <*@RoomTypeCo 1  Str Code of the Room.
  de>\*            ing 

  <*@InvBlockCo 1  Str Inventary block code.
  de>\*            ing 

  <*@RatePlanCo 1  Str Code of the RatePlan.
  de>\*            ing 

  RoomRate/Rate 1      Node containing information about the rates.
  s                    

  Rates/Rate    1      Node containing information about one rate.

  <*@EffectiveD 1  Dat Effective date when the Rate start applying.
  ate>\*           e   

  <*@ExpireDate 1  Dat Expire date when the Rate ends applying.
  >\*              e   

  Rate/Base     1      Node containing core information about the rate.

  <*@AmountBefo 0. Dec Amount before tax of the rate.
  reTax>\*      .1 ima 
                   l   

  <*@AmountAfte 1  Dec Amount after tax of the rate.
  rTax>\*          ima 
                   l   

  <*@CurrencyCo 1  Str Currency code of the rate.
  de>\*            ing 

  Rate/CancelPo 1      Node containing information about cancel policies
  licies               which are applied to the rate.

  CancelPolicie 0.     Node containing information about one cancel
  s/CancelPenal .n     penalty.
  ty                   

  <*@PolicyCode 1  Str Policy code of the cancel penalty.
  >\*              ing 

  RoomRate/Tota 1      Node containing information about the total price
  l                    of the RoomRate.

  <*@AmountBefo 0. Dec Amount before tax of the RoomRate.
  reTax>\*      .1 ima 
                   l   

  <*@AmountAfte 1  Dec Amount after tax of the RoomRate.
  rTax>\*          ima 
                   l   

  <*@CurrencyCo 1  Str Currency code of the RoomRate.
  de>\*            ing 

  RoomStay/Canc 1      Node containing all cancel penalties of the
  elPenalties          RoomStay.

  CancelPenalti 0.     Node containing information about one cancel
  es/CancelPena .n     penalty.
  lty                  

  <*@PolicyCode 1  Str Policy code of the cancel penalty.
  >\*              ing 

  <*@NonRefunda 1  Boo Indicates whether the Rate is refundable or not.
  ble>\*           lea 
                   n   

  CancelPenalty 0.     Node containing information about the deadline of
  /Deadline     .n     the cancel penalty.

  <*@AbsoluteDe 1  Dat Indicates when the absolute deadline.
  adline>\*        eTi 
                   me  

  <*@OffsetTime 1  Str Time unit of the offset for the absolute deadline.
  Unit>\*          ing 

  <*@OffsetUnit 1  Int Number of time units of offset for the absolute
  Multiplier>\*    ege deadline.
                   r   

  <*@OffsetDrop 1  Str Indicates when the deadline is applied.
  Time>\*          ing 

  CancelPenalty 0.     Amount of the cancel penalty.
  /AmountPercen .n     
  t                    

  <*@Percent>\* 1  Str Percent of the total charged as a cancel penalty
                   ing amount. Percent or NmbrOfNights must be present.

  <*@NmbrOfNigh 1  Str Number of nights charged as a cancel penalty
  ts>\*            ing amount.

  <*@CurrencyCo 1  Str Currency code of the cancel penalty amount.
  de>\*            ing 

  RoomStay/Basi 1      Node containing basic information of the property.
  cPropertyInfo        

  RoomStay/Serv 1      Node containing information of the guests of the
  iceRPHs              room.

  ServiceRPHs/S 1.     Node containing information of a guest of the room.
  erviceRPH     .n     

  <*@RPH>\*     1  Str Code of a guest of the room. Match with
                   ing <*@ResGuestRPH>\* at the ResGuests node.

  HotelCode     1  Int Hotel code.
                   ege 
                   r   

  HotelName     1  Str Hotel name.
                   ing 

  HotelReservat 1      Node containing all reservation guests.
  ion/ResGuests        

  ResGuests/Res 1.     Node containing information about one of the
  Guest         .n     guests.

  ResGuest/ResG 1.     Node containing information about one of the
  uest          .n     guests.

  <*@ResGuestRP 1  Int RPH of the guest.
  H>\*             ege 
                   r   

  <*@AgeQualify 1  Int Age qualifying code of the guest.
  ingCode>\*       ege 
                   r   

  ResGuest/Prof 1      Node containing information about the profiles of
  iles                 the guest.

  Profiles/Prof 1      Node containing information about the profile of
  ileInfo              the guest.

  ProfileInfo/C 1      Node containing customer information of the guest.
  ustomer              

  Customer/Pers 1      Node containing the person name of the guest.
  onName               

  PersonName/Na 1  Str Prefix/Traitement name of the guest.
  mePrefix         ing 

  PersonName/Gi 1  Str Given name of the guest.
  venName          ing 

  PersonName/Su 1  Str Surname of the guest.
  rname            ing 

  ResGuest/Gues 1      Node containing quantity informations for the
  tCounts              guest.

  GuestCounts/G 1      Node containing quantity information for the guest.
  uestCount            

  <*@Age>\*     1  Int Age of the guest.
                   ege 
                   r   

  ResGlobalInfo 1      Node containing general information about the
                       reservation.

  ResGlobalInfo 1      Node containing the total price.
  /Total               

  <*@AmountBefo 0. Dec Amount before tax of the Reservation.
  reTax>\*      .1 ima 
                   l   

  <*@AmountAfte 1  Dec Amount after tax of the Reservation.
  rTax>\*          ima 
                   l   

  <*@CurrencyCo 1  Str Currency code of the Reservation.
  de>\*            ing 

  ResGlobalInfo 0.     Node containing the Guarantee provided with the
  /Guarantee    .1     reservation.

  <*@PaymentCod 1      Contains the payment method accepted by the rate.
  e>\*                 See Payment Type Codes list in section 7.6.3.

  Guarantee/Gua 0.     Node containing the Guarantee provided with the
  ranteesAccept .1     reservation.
  ed                   

  GuaranteesAcc 1      Node that contains the booking payment details
  epted/Guarant        accepted.
  eeAccepted           

  GuaranteeAcce 1      Node that contains the credit card accepted. The
  pted/PaymentC        credit card information can be a URL with the
  ard                  information(in TPA\_Extension tag) or the details
                       in the PaymentCard tags and attributes.

  <*@CardCode>\ 1  Str Contains the credit card code. See Credit Card
  *                ing Codes list in section 7.6.4.

  <*@ExpireDate 0. Str This is the expiry date of the credit card used for
  >\*           .1 ing deposit/prepayment. Format MMyy.

  PaymentCard/C 0. Str PaymentCard / CardHolderName
  ardHolderName .1 ing 

  PaymentCard/C 0. Str This is actual number of the credit card used for
  ardNumber/Pla .1 ing deposit/prepayment.
  inText               

  PaymentCard/S 0. Str The SeriesCode attribute is used (Optionally) for
  eriesCode/Pla .1 ing the security number of the card.
  inText               

  PaymentCard/T 0.     Optional, contains credit card URL.
  PA\_Extension .1     
  s                    

  Param         1      

  <*@key>\*     1  Str URL
                   ing 

  <*@value>\*   1  Str URL where the Credit card details are stored.
                   ing 

  ResGlobalInfo 1      Node containing the ids of the reservation.
  /HotelReserva        
  tionIDs              

  HotelReservat 2      Node containing information of one reservation id.
  ionIDs/HotelR        
  eservationID         

  <*@ResID*>Val 1  Str Value of the id.
  ue\_             ing 

  <*@ResID*>Sou 1  Str Id context.
  rceContext\_     ing 

  ResGlobalInfo 1      Node containing information about the profiles of
  /Profiles            the reservation.

  Profiles/Prof 1      Node containing information about the profile of
  ileInfo              the reservation.

  ProfileInfo/P 1      Node containing information about the profile of
  rofile               the reservation.

  Profile/Custo 1      Node containing information about the customer of
  mer                  the reservation. The customer of the reservation
                       can be or not a pax of the reservation. If it's a
                       pax will be present in ResGuests node.

  Customer/Pers 1      Node containing the person name of the customer of
  onName               the reservation.

  PersonName/Na 1  Str Name prefix of the customer.
  mePrefix         ing 

  PersonName/Gi 1  Str Given name of the customer.
  venName          ing 

  PersonName/Su 1  Str Surname of the customer.
  rname            ing 

  Customer/Tele 1      Node containing information about the telephone of
  phone                the customer.

  <*@PhoneTechT 1  Str Phone technology type.
  ype>\*           ing 

  <*@PhoneNumbe 1  Str Phone number.
  r>\*             ing 

  <*@FormattedI 1  Str Indicates whether associated data is formatted or
  nd>\*            ing not.

  <*@DefaultInd 1  Str When true, indicates a default value should be
  >\*              ing used.

  Customer/Emai 1      Node containing information about the email of the
  l                    customer.

  <*@DefaultInd 1  Str When true, indicates a default value should be
  >\*              ing used.

  <*@EmailType> 1  Str Indicates the type of the email.
  \*               ing 

  Value         1  Str Email of the customer.
                   ing 

  Customer/Addr 1      Node containing information about the address of
  ess                  the customer.

  Address/Addre 1  Str Address of the customer.
  ssLine           ing 

  Address/CityN 1  Str City name.
  ame              ing 

  Address/Posta 1  Str Postal code.
  lCode            ing 

  Address/State 1  Str Node containing information about the state or the
  Prov             ing province of the customer.

  <*@StateCode> 1  Str State code.
  \*               ing 

  Value         1  Str State or province name.
                   ing 

  Address/Count 1  Str Country name.
  ryName           ing 

  <*@Code>\*    1  Str Country code.
                   ing 

  Value         1  Str Country name.
                   ing 
  ------------------------------------------------------------------------

**Example Guarantee object with credit card details**

    <Guarantee PaymentCode="DirectPayment">
      <GuaranteesAccepted>
        <GuaranteeAccepted>
          <PaymentCard ExpireDate="0614" CardCode ="VI">
            <CardHolderName>John Smith</CardHolderName>
            <CardNumber>
              <PlainText>4321432143214327</PlainText>
            </CardNumber>
            <SeriesCode>
              <PlainText>123</PlainText>
            </SeriesCode>
          </PaymentCard>
        </GuaranteeAccepted>
      </GuaranteesAccepted>
    </Guarantee>

**Example Guarantee object with URL for credit card details**

    <Guarantee PaymentCode="DirectPayment">
      <GuaranteesAccepted>
        <GuaranteeAccepted>
          <PaymentCard>
            <TPA_Extensions>
              <Param key = "URL" value = "http://www.exampleUrl.com/"/>
            </TPA_Extensions>
          </PaymentCard>
        </GuaranteeAccepted>
      </GuaranteesAccepted>
    </Guarantee>

|