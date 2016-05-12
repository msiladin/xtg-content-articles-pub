---
title: StaticConfiguration
keywords: hotel, data structure, static configuration, static
sidebar: mydoc_sidebar
permalink: /developer-documentation/hotel/DSF/StaticConfiguration
---

|

Method Goals
============

This message provides information about the static configuration of the
provider, to see and configure the provider in the best way.

|

Request Format
==============

The request does not require any elements empty request.

|

Response Format
===============

The XML returned contains more elements on the configuration (number of
hotels, the number of cities and the number of areas of availability, if
the provider returns the cancellation policies, maximum number of
distributions, maximum number of paxes in a distribution, release days,
stay minimum, list of languages that allows ....).

|

StaticConfigurationRQ Example
=============================

    <StaticConfigurationRQ>
    </StaticConfigurationRQ>

|

StaticConfigurationRQ Description
=================================

  ------------------------------------------------------------------------
  Element     Numbe Type  Description
              r           
  ----------- ----- ----- ------------------------------------------------
  StaticConfi 1           Root node.
  gurationRQ              
  ------------------------------------------------------------------------

|

StaticConfigurationRS Example
=============================

    <StaticConfigurationRS>
        <MaxNumberHotels>2000</MaxNumberHotels>
        <MaxNumberCities>1</MaxNumberCities>
        <MaxNumberZones>1</MaxNumberZones>
        <MaxNumberGeoCodes>0</MaxNumberGeoCodes>
        <RequiredRoomList>false</RequiredRoomList>
        <InformCancelPolicies>true</InformCancelPolicies>
        <InformBindingPriceValuation>true</InformBindingPriceValuation>
        <InformBindingPrice>true</InformBindingPrice>
        <InformNRFValuation>true</InformNRFValuation>
        <InformNRFRate>true</InformNRFRate>
        <Inform55Rate>true</Inform55Rate>
        <InformPackageRate>true</InformPackageRate>
        <InformExtraActivity>false</InformExtraActivity>
        <InformForfait>true</InformForfait>
        <RemarksValuation>true</RemarksValuation>
        <MaxNumberRoomCandidates>9</MaxNumberRoomCandidates>
        <MaxPaxInRoomCandidates>9</MaxPaxInRoomCandidates>
        <Release>0</Release>
        <MinimumStay>0</MinimumStay>
        <InformBillingSupplierReservation>false</InformBillingSupplierReservation>
        <ImplementsProvideLocatorReservationRead>true</ImplementsProvideLocatorReservationRead>
        <ImplementsClientLocatorReservationRead>true</ImplementsClientLocatorReservationRead>
        <ImplementsCancel>true</ImplementsCancel>
        <InformPriceReservation>true</InformPriceReservation>
        <HotelListLanguages>
            <Languages>
                <Language>en</Language>
                <Language>es</Language>
                <Language>de</Language>
                <Language>pt</Language>
                <Language>fr</Language>
                <Language>it</Language>
            </Languages>
        </HotelListLanguages>
        <ReservationListCreationDate>true</ReservationListCreationDate>
        <ReservationListCheckDate>true</ReservationListCheckDate>
        <HotelListType>OffLineCompleted</HotelListType>
        <DescriptiveInfoType>NotImplemented</DescriptiveInfoType>
        <GeographicDestinationTreeType>OffLine</GeographicDestinationTreeType>
        <AvailDestinationTreeType>OffLine</AvailDestinationTreeType>
        <RoomListType>OnLine</RoomListType>
        <InformCancelPoliciesReservationRead>false</InformCancelPoliciesReservationRead>
        <InformCancelPoliciesReservationList>false</InformCancelPoliciesReservationList>
        <InformCancelPoliciesAvail>false</InformCancelPoliciesAvail>
        <InformChangesPolicies>false</InformChangesPolicies>
        <ImplementsDeltaPrice>false</ImplementsDeltaPrice>
        <RequiredAllPassengers>true</RequiredAllPassengers>
        <InformBedsAvail>false</InformBedsAvail>
        <InformModificationPolicies>false</InformModificationPolicies>
        <ModifyTransactions>
            <ModifyTransaction>
                <Modify>ModifyStartDateAddDays</Modify>
                <Modify>ModifyEndDateAddDays</Modify>
            </ModifyTransaction>
            <ModifyTransaction>
                <Modify>ModifyHolder</Modify>
                <Modify>ModifyRoomsAddRooms</Modify>
                <Modify>ModifyRoomsRemoveRooms</Modify>
            </ModifyTransaction>
        </ModifyTransactions>
        <AllowsCurrencyAvail>true</AllowsCurrencyAvail>
        <InformCancelPoliciesModify>false</InformCancelPoliciesModify>
        <AllowOnRequest>false</AllowOnRequest>
        <ImplementsDailyRatePlan>false</ImplementsDailyRatePlan>
        <AllowRemarks>false</AllowRemarks>
        <InformSharedBed>false</InformSharedBed>
        <InformBedType>false</InformBedType>
        <InformNumberOfBeds>false</InformNumberOfBeds>  
        <AllowBlockOption>false</AllowBlockOption>  
        <InformExclusiveDeal>false</InformExclusiveDeal>    
        <InformPriceCancel>false</InformPriceCancel>
        <AllowUrlCard>false</AllowUrlCard>
        <InformCancelPoliciesDescription>false</InformCancelPoliciesDescription>        
        <PaymentTypes>
             <PaymentType>LaterPay</PaymentType>
             <PaymentType>MerchantPay</PaymentType>
        </PaymentTypes>     
        <InformAvailableModificationsInReservationRead>false</InformAvailableModificationsInReservationRead>    
        <RequiredNationality>false</RequiredNationality>    
        <Inform60Rate>false</Inform60Rate>
        <Inform65Rate>false</Inform65Rate>
        <InformCanaryResidentRate>false</InformCanaryResidentRate>
        <InformBalearicResidentRate>false</InformBalearicResidentRate>
        <InformLargeFamilyRate>false</InformLargeFamilyRate>
        <InformHoneymoonRate>false</InformHoneymoonRate>        
        <ImplementsBusinessRules>false</ImplementsBusinessRules>    
        <ImplementsProviderLocatorCancel>false</ImplementsProviderLocatorCancel>    
        <ImplementsClientLocatorCancel>false</ImplementsClientLocatorCancel>            
        <NumMarketsAllowed>5</NumMarketsAllowed>            
        <InformTiket>false</InformTiket>
        <ImplementsDescriptiveInfoExtended>false</ImplementsDescriptiveInfoExtended>
        <InformNumberOfUnits>true</InformNumberOfUnits>     
    </StaticConfigurationRS>

|

StaticConfigurationRS Description
=================================

  --------------------------------------------------------------------------
  Element               Numb Type Description
                        er        
  --------------------- ---- ---- ------------------------------------------
  StaticConfigurationRS 1         Root node.

  MaxNumberHotels       1    Inte Maximum number of hotel that can be
                             ger  requested in a avail petition.

  MaxNumberCities       1    Inte Maximum number of cities that can be
                             ger  requested in a avail petition.

  MaxNumberZones        1    Inte Maximum number of zones that can be
                             ger  requested in a avail petition.

  MaxNumberGeoCodes     1    Inte Maximum number of GeoCodes that can be
                             ger  requested in a avail petition.

  RequiredRoomList      1    Bool The provider has implemented a list of
                             ean  rooms, where the provider will return the
                                  description of the room in availability,
                                  not a mandatory call.

  InformCancelPolicies  1    Bool The provider informs of the cancellation
                             ean  policies.

  InformBindingPriceVal 1    Bool Informs if the price of the option in the
  uation                     ean  response of valuation is binding.

  InformBindingPrice    1    Bool Provider returns binding PVPs in
                             ean  availability.

  InformNRFValuation    1    Bool The provider can inform in valuation if
                             ean  the rate is non-refundable.

  InformNRFRate         1    Bool The provider can inform in availability if
                             ean  the rate is non-refundable.

  InformNRFRateByRoom   1    Bool The provider can inform in availability if
                             ean  the room is non-refundable.

  Inform55Rate          1    Bool The provider informs the options with
                             ean  rates of pax of 55 years old or over in
                                  availability.

  InformPackageRate     1    Bool The provider informs the options with
                             ean  package rates in availability. These
                                  options cant be sold by separate, need to
                                  add a service (like a plane ticket).

  InformExtraActivity   1    Bool The provider informs of the possible
                             ean  option type Hotel+entrance.

  InformForfait         1    Bool The provider informs of the possible
                             ean  option type Hotel+Forfait.

  RemarksValuation      1    Bool The provider informs of the important
                             ean  observation in policies, like per example,
                                  supplies paid in the hotel.

  MaxNumberRoomCandidat 1    Inte Maximum number of room candidates that can
  es                         ger  be requested in the same avail request.

  MaxPaxInRoomCandidate 1    Inte Maximum number paxs in same room that can
  s                          ger  be requested in the same avail request.

  Release               1    Inte Minimum days that is required in between
                             ger  booking date and checking date ( days in
                                  advance ). If the value is zero then there
                                  is no limitation.

  MinimumStay           1    Inte Minimum number of days that are needed to
                             ger  be booked. If the value is zero then there
                                  is no limitation.

  InformBillingSupplier 1    Bool Informs of the data of the external
  Reservation                ean  provider in the booking.

  ImplementsProvideLoca 1    Bool The provider implements the consult
  torReservationRead         ean  transaction with the **provider**
                                  localizator.

  ImplementsClientLocat 1    Bool The provider implements the consult
  orReservationRead          ean  transaction with the **client**
                                  localizator.

  ImplementsCancel      1    Bool The provider implements cancellation
                             ean  transaction.

  InformPriceReservatio 1    Bool The provider informs about the price in
  n                          ean  the reservation in the booking RS.

  HotelListLanguages    1         Languages that the provider can return
                                  their information.

  HotelListLanguages/La 1         Languages.
  nguages                         

  HotelListLanguages/La 1..n Stri Languages description.
  nguages/Language           ng   

  ReservationListCreati 1    Bool The provider implements the list of
  onDate                     ean  bookings transaction by creation date.

  ReservationListCheckD 1    Bool The provider implements the list of
  ate                        ean  bookings transaction by check in date.

  HotelListType         1    Enum See the specification in
                                  Static-Type section\_.

  DescriptiveInfoType   1    Enum See the specification in
                                  Static-Type section\_.

  GeographicDestination 1    Enum See the specification in
  TreeType                        Static-Type section\_.

  AvailDestinationTreeT 1    Enum See the specification in
  ype                             Static-Type section\_.

  RoomListType          1    Enum See the specification in
                                  Static-Type section\_.

  InformCancelPoliciesR 1    Bool Informs of the cancellation policies in
  eservationRead             ean  the booking consultation.

  InformCancelPoliciesR 1    Bool Informs of the cancellation policies in
  eservationList             ean  the booking list.

  InformCancelPoliciesA 1    Bool Informs of the cancellation policies in
  vail                       ean  availability.

  InformChangesPolicies 1    Bool The provider informs if there is an extra
                             ean  fee for any booking modification.

  ImplementsDeltaPrice  1    Bool Implemented a margin stipulated by the
                             ean  client for booking with a higher price
                                  (delta).

  RequiredAllPassengers 1    Bool Needs all of the data (names and surnames)
                             ean  of all the pax in booking.

  ImplementsOffersAvail 1    Bool If it shows in availability the applied
                             ean  offers.

  ImplementsRemarksAvai 1    Bool Observation and comments.
  l                          ean  

  AllowsCurrencyAvail   1    Bool If true, then it is possible to indicate
                             ean  the currency on a availability level.

  AllowOnRequest        1    Bool If true, then the provider specifies the
                             ean  on request status option on a
                                  availability, valuation, or reservation
                                  level.

  InformCancelPoliciesM 1    Bool Informs of the cancellation policies in
  odify                      ean  Modification call.

  ImplementsDailyPrice  1    Bool Specifies if the provider return the daily
                             ean  price in availability call.

  ImplementsDailyRatePl 1    Bool Specifies if the provider return the daily
  an                         ean  rate in availability call.

  AllowRemarks          1    Bool Specifies if the provider allows send
                             ean  remarks in Reservation request.

  InformSharedBed       1    Bool Specifies if the provider informs in
                             ean  availability response if beds in the room
                                  are shared.

  InformBedType         1    Bool Specifies if the provider informs in
                             ean  availability response the beds types.

  InformNumberOfBeds    1    Bool Specifies if the provider informs in
                             ean  availability response the number of beds
                                  for each room.

  AllowBlockOption      1    Bool Specifies if the provider block the option
                             ean  in valuation call.

  InformExclusiveDeal   1    Bool The provider indicates in one Hotel is an
                             ean  Exclusive Deal in HotelList and/or
                                  DescriptiveInfo.

  InformPriceCancel     1    Bool The provider informs about the cancelation
                             ean  price in the cancel response.

  AllowUrlCard          1    Bool Specifies if the provider allows url card
                             ean  data encode when the option type is
                                  LaterPay.

  InformCancelPoliciesD 1    Bool Specifies if the provider inform the
  escription                 ean  cancel policies in free text in Valuation
                                  response.

  ImplementsBusinessRul 1    Bool Specifies if in this provider use the
  es                         ean  business rules in availability.

  PaymentTypes          1         List of payment types accepted by the
                                  supplier.

  PaymentTypes/PaymentT 1..n      Indicates the typology of payment
  ype                             (Merchant, Direct ...) .

  InformAvailableModifi 1    Bool Specifies if the provider inform the
  cationsInReservationR      ean  available modifications in
  ead                             ReservationReadRS.

  RequiredNationality   1    Bool Specifies if the provider required the
                             ean  nationality in Avail, Valuation and
                                  Reservation call.

  Inform60Rate          1    Bool The provider informs the options with
                             ean  rates of pax of 60 years old or over in
                                  availability.

  Inform65Rate          1    Bool The provider informs the options with
                             ean  rates of pax of 65 years old or over in
                                  availability.

  InformCanaryResidentR 1    Bool The provider informs the options with
  ate                        ean  canary resident rates in availability.
                                  These options cant be sold if the customer
                                  don't have this condition.

  InformCanaryResidentR 1    Bool The provider informs the options with
  ate                        ean  balearic resident rates in availability.
                                  These options can't be sold if the
                                  customer don't have this condition.

  InformBalearicResiden 1    Bool The provider informs the options with
  tRate                      ean  large family rates in availability. These
                                  options can't be sold if the customer
                                  don't have this condition.

  InformLargeFamilyRate 1    Bool The provider informs the options with
                             ean  canary resident rates in availability.
                                  These options can't be sold if the
                                  customer don't have this condition.

  InformHoneymoonRate   1    Bool The provider informs the options with
                             ean  honeymoon rates in availability. These
                                  options can't be sold if the customer
                                  don't have this condition.

  ImplementsProviderLoc 1    Bool The provider implements the cancel
  atorCancel                 ean  transaction with the **provider**
                                  localizator.

  ImplementsClientLocat 1    Bool The provider implements the cancel
  orCancel                   ean  transaction with the **client**
                                  localizator.

  InformModificationPol 1    Bool The provider informs of the modification
  icies                      ean  policies in Valuation process.

  ModifyTransactions    0..1      Modifications allowed by the supplier.

  ModifyTransactions/Mo 1..n      Modifications set allowed in the same
  difyTransaction                 request by the supplier.

  ModifyTransactions/Mo 1..n      Modification type (ModifyStartDateAddDays,
  difyTransaction/Modif           ModifyStartDateSubtractDays,
  y                               ModifyEndDateAddDays,
                                  ModifyEndDateSubtractDays, ModifyHolder,
                                  ModifyRoomsAddRooms,
                                  ModifyRoomsRemoveRooms, ModifyMealPlan or
                                  ModifyAddComment).

  NumMarketsAllowed     1    Inte Number of markets that the provider
                             ger  support in the same request.

  InformTiket           1    Bool The provider informs of the possible
                             ean  option type Hotel+Tiket.

  ImplementsDescriptive 1    Bool It indicates whether the new
  InfoExtended               ean  DescriptiveInfo is implemented.

  InformNumberOfUnits   1    Bool The provider inform the number of units
                             ean  are available per room.
  --------------------------------------------------------------------------

|

Detailed description
====================

**HotelListType, DescriptiveInfoType, GeographicDestinationTreeType,
AvailDestinationTreeType and RoomListType:**

If the parameter value is set as online, then the information of these
methods is obtained of the supplier system. On the other hand if the
parameter takes antoher value means that the process takes more than 4
minutes. In this case, we need to load the information process in our
BBDD. Information of these methods are updated every week.

|

In case that the provider return the status in process response in
avail, valuation or reservation you can filter this option if you send
the parameter \<OnRequest\>true\</OnRequest\>.

By default the following tags:

-   **ImplementsDailyRatePlan**
-   **InformSharedBed**
-   **InformBedType**
-   **InformNumberOfBeds**
-   **AllowBlockOption**
-   **InformPriceCancel**
-   **InformAvailableModificationsInReservationRead**
-   **RequiredNationality**
-   **Inform60Rate**
-   **Inform65Rate**
-   **InformCanaryResidentRate**
-   **InformBalearicResidentRate**
-   **InformLargeFamilyRate**
-   **InformHoneymoonRate**
-   **ImplementsProviderLocatorCancel**
-   **ImplementsClientLocatorCancel**
-   **NumMarketsAllowed**
-   **ImplementsDescriptiveInfoExtended**
-   **InformNumberOfUnits**

Rigth now, this tags are set up to false value, either because the
provider doesn't support it or because is not updated yet.

|