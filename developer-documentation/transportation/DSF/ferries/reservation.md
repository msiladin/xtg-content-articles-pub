---
title: Reservation
keywords: transportation, data structure, ferries, reservation
sidebar: mydoc_sidebar
permalink: /developer-documentation/transportation/DSF/ferries/reservation
---

|

Method Goals
============

This method aims to book one or more itineraries.

|

Request Format
==============

The request format works the same way as the Valuation request. It can
work with one Itinerary or with two.

This request also holds the passengers and payment data.

|

Response Format
===============

The result returns a list of Locator (booking codes). It can be the
supplier's or the one sent in the request. It also returns all the
charges associated to the booking.

|

Remarks
=======

|

ReservationRQ ---------

:

    <ReservationRQ>
    <Itineraries>
        <Itinerary id = "0">
            <Conditions>
                <Condition id = "0" language = "ES">
                    <Text>CAFETERIA#CAFETERIA##RTN#TARIFA IDA Y VUELTA#F0-TRAYECTO SIN RESTRICCIONES#F0#2.09</Text>
                </Condition>
                <Condition id = "1" language = "ES">
                    <Text>CAFETERIA#CAFETERIA##RTN#TARIFA IDA Y VUELTA#F0-TRAYECTO SIN RESTRICCIONES#F0#1.87</Text>
                </Condition>
            </Conditions>
            <Journeys>
                <Journey id = "0" Duracion = "0">
                    <Segments>
                        <Segment id = "0">
                            <SegmentInfo
                                id = "1"
                                transportationId = "BJ1#VISEMAR ONE#FERRY"
                                transportationType = "F"
                                operatingCarrier = "BAL"
                                marketingCarrier = "BAL"
                                departureTerminal = "PAL"
                                arrivalTerminal = "VAL"
                                departureDate = "2015-08-27T11:30:00"
                                arrivalDate = "2015-08-27T19:30:00"
                                transportationName = "VISEMAR ONE"
                                transportationCode = "BJ1"
                                segmentStatus = "HK"
                                tieneParadaTecnica = "false">
                                <OriginLoc type = "P" code = "PAL" citycode = "false"/>
                                <DestinationLoc type = "P" code = "VAL" citycode = "false"/>
                            </SegmentInfo>
                            <SegmentClasses>
                                <SegmentClass cabinClass = "N" class = "CAFETERIA" paxRef = "0" fareType = "PUB">
                                    <CancellationPolicies>
                                        <CancellationPolicy amount = "0" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-19T10:16:00" refundable = "true"/>
                                        <CancellationPolicy amount = "10" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-20T11:30:00" refundable = "true"/>
                                        <CancellationPolicy amount = "20" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-25T11:30:00" refundable = "true"/>
                                        <CancellationPolicy amount = "100" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-27T11:30:00" refundable = "true"/>
                                    </CancellationPolicies>
                                    <Modifiable modifiable = "true" amount = "0" currency = "EUR" amountType = "AMOUNT">
                                        <Description>Admite cambios sin cargos</Description>
                                    </Modifiable>
                                </SegmentClass>
                            </SegmentClasses>
                        </Segment>
                    </Segments>
                </Journey>
                <Journey id = "0" Duracion = "0">
                    <Segments>
                        <Segment id = "0">
                            <SegmentInfo
                                id = "2"
                                transportationId = "BJ1#VISEMAR ONE#FERRY"
                                transportationType = "F"
                                operatingCarrier = "BAL"
                                marketingCarrier = "BAL"
                                departureTerminal = "VAL"
                                arrivalTerminal = "PAL"
                                departureDate = "2015-09-04T22:15:00"
                                arrivalDate = "2015-09-05T06:00:00"
                                transportationName = "VISEMAR ONE"
                                transportationCode = "BJ1"
                                segmentStatus = "HK"
                                tieneParadaTecnica = "false">
                                <OriginLoc type = "P" code = "VAL" citycode = "false"/>
                                <DestinationLoc type = "P" code = "PAL" citycode = "false"/>
                            </SegmentInfo>
                            <SegmentClasses>
                                <SegmentClass cabinClass = "N" class = "CAFETERIA" paxRef = "0" fareType = "PUB">
                                    <CancellationPolicies>
                                        <CancellationPolicy amount = "0" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-19T10:16:00" refundable = "true"/>
                                        <CancellationPolicy amount = "10" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-28T22:15:00" refundable = "true"/>
                                        <CancellationPolicy amount = "20" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-09-02T22:15:00" refundable = "true"/>
                                        <CancellationPolicy amount = "100" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-09-04T22:15:00" refundable = "true"/>
                                    </CancellationPolicies>
                                    <Modifiable modifiable = "true" amount = "0" currency = "EUR" amountType = "AMOUNT">
                                        <Description>Admite cambios sin cargos</Description>
                                    </Modifiable>
                                </SegmentClass>
                            </SegmentClasses>
                        </Segment>
                    </Segments>
                </Journey>
            </Journeys>
            <AmountBreakdown currency = "EUR" totalAmount = "420" nonCommissionableAmount = "0" commission = "0.942857142857136">
                <ChargeBreakdowns>
                    <ChargeBreakdown type = "VEHICLE" amount = "269.0" currency = "EUR">
                        <Concept id = "0" language = "ES">
                            <Texto>PRECIO VEHICULO</Texto>
                        </Concept>
                    </ChargeBreakdown>
                    <ChargeBreakdown type = "VEHICULE_FEE" amount = "11" currency = "EUR">
                        <Concept id = "1" language = "ES">
                            <Text>FEE VEHICULO</Text>
                        </Concept>
                    </ChargeBreakdown>
                </ChargeBreakdowns>
                <PaxBreakdowns>
                    <PaxBreakdown paxType = "ADT" amount = "140" taxes = "11" currency = "EUR"/>
                </PaxBreakdowns>
            </AmountBreakdown>
            <PaxConfigurations>
                <PaxConfiguration id = "0" paxRef = "0" age = "30" paxType = "ADT">
                    <AppliedBonuses resident = "N" largeFamily = "N" discountCard = "N"/>
                </PaxConfiguration>
            </PaxConfigurations>
            <VehicleConfigurations>
                <VehicleConfiguration vehicleRef = "1" height = "160" length = "350" type = "Tourism" code = "T1" name = "Turismo"/>
            </VehicleConfigurations>
        </Itinerary>
    </Itineraries>
    <Passengers>
        <Passenger
            id = "0"
            passengerType = "MR"
            name = "TestName"
            surname = "TestSurname"
            birthDate = "1985-08-19T12:11:38.577517+02:00"
            documentType = "NATIONAL_ID"
            documentId = "44183932N"
            documentExpiration = "2015-08-19T12:15:33.503954+02:00"
            documentExpedition = "0001-01-01T00:00:00"
            nationality = "ESP"
            gender = "72">
            <PaxBonusDetails>
                <AppliedBonuses resident = "N" largeFamily = "N" discountCard = "N"/>
                <ResidentCityCode>070146</ResidentCityCode>
                <LargeFamilyId/>
                <LargeFamilyCityCode/>
                <ResidentCertificateId>1234567890</ResidentCertificateId>
            </PaxBonusDetails>
        </Passenger>
    </Passengers>
    <Vehicles>
        <Vehicle licensePlate = "0000abc" brand = "testMarca" model = "testModelo" code = "T1" height = "160" length = "350" type = "Tourism"/>
    </Vehicles>
    <Client passengerType = "MR" name = "TestNom" surname = "TestApe" eMail = "transportation@xmltravelgate.com" countryPrefix = "+34" telephone = "+34 858 275 617" mobilephone = "+34 858 275 617">
        <Address zipCode = "12159" countryCode = "es">
            <Street>C/ test, 28</Street>
            <City>test</City>
        </Address>
    </Client>
    <Locators>
        <Locator>
            <Id>123456</Id>
            <Type>PROVEEDOR</Type>
        </Locator>
    </Locators>
    <DeltaPrice>0</DeltaPrice>

\</ReservationRQ\>

|

ReservationRQ Description
=========================

  -------------------------------------------------------------------------
  Element                      Nu Typ Description
                               mb e   
                               er     
  ---------------------------- -- --- -------------------------------------
  ReservationRQ                1      Root node..

  Passengers                   1      Paxes information.

  Passengers/Passenger         1.     List of Passenger.
                               .n     

  <*@passengerType>\*          1  Str Possible values: MR, MRS, CHD, INF.
                                  ing 

  <*@name>\*                   1  Str Name of the passenger.
                                  ing 

  <*@surname>\*                1  Str Surname of the passenger.
                                  ing 

  <*@birthDate>\*              1  Dat Date of birth of the passenger.
                                  e   

  <*@documentType>\*           1  Str Possible values: NATIONAL\_ID,
                                  ing PASSPORT, RESIDENT\_ID,
                                      FOREIGN\_PASSPORT.

  <*@documentId>\*             1  Str Document ID.
                                  ing 

  <*@documentExpiration>\*     1  Dat Date of expiration of the document.
                                  e   

  <*@documentExpedition>\*     1  Dat Date of expedition of the document.
                                  e   

  <*@nationality>\*            1  Str Nationality code (ISO 3166-1
                                  ing alphaa-3)

  <*@gender>\*                 1  Cha Possible values: 72 (male), 77
                                  r   (female).

  Passenger/PaxBonusDetails    1      Details of the discount bonus applied
                                      to the passenger.

  Passenger/PaxBonusDetails/Ap 0.     Applied discounts.
  pliedBonuses                 .1     

  <*@resident>\*               1      Resident discount type: N(None),
                                      BP(Balearic Islands resident flying
                                      to mainland), BI(Balearic Islands
                                      resident flying to another balearic
                                      island), DC(Canarian Islands resident
                                      flying to another Canarian Island),
                                      RC(Canarian Islands resident flying
                                      to mainland),RM(Ceuta/Melilla
                                      resident), STR(Italian resident
                                      discount), ELB(Italian resident
                                      Elba), SDG(Italian resident
                                      Sardegna), SCL(Italian resident
                                      Sicily).

  <*@largeFamily>\*            1  Str Family discount type: N(None),
                                  ing F1(Large family), F2 (Special large
                                      family).

  <*@discountCard>\*           1  Str Discount card type (for more details,
                                  ing see information below).

  Passenger/PaxBonusDetails/Re 0. Str If required, city code for the
  sidentCityCode               .1 ing Spanish Resident discount.

  Passenger/PaxBonusDetails/La 0. Str Mandatory if customer wants to apply
  rgeFamilyId                  .1 ing Spanish family discount.

  Passenger/PaxBonusDetails/La 0. Str City code for the Spanish Family
  rgeFamilyCityCode            .1 ing discount.

  Passenger/PaxBonusDetails/Re 0. Str Mandatory if requested Spanish
  sidentCertificateId          .1 ing Resident discount.

  Itineraries                  1      List of Itineraries.

  Itineraries/Itinerary        1.     Details of the Itinerary.
                               .n     

  <*@id>\*                     1  Int Unique identifier of the Itinerary.
                                  ege 
                                  r   

  <*@fareRef>\*                1  Int Reference identifier to the original
                                  ege Fare. Flights parameter.
                                  r   

  Itineraries/Itinerary/Condit 0.     Contains a list of Conditions.
  ions                         .1     

  Itineraries/Itinerary/Journe 0.     Contains a list of Journeys.
  ys                           .1     

  Itineraries/Itinerary/Journe 0.     Contains details of the Journeys.
  ys/Journey                   .n     

  <*@id>\*                     1  Int Unique identifier of the Journey in
                                  ege scope.
                                  r   

  <*@duration>\*               1  Int Duration of the Journey in minutes.
                                  ege 
                                  r   

  Itineraries/Itinerary/Journe 0.     Contains a list of Segments
  ys/Journey/Segments          .1     associated to the Journey.

  Itineraries/Itinerary/Journe 0.     Contains details of the SegmentInfo.
  ys/Journey/Segments/Segment  .n     

  <*@id>\*                     1  Int Unique SegmentInfo identifier.
                                  ege 
                                  r   

  Itineraries/Itinerary/Journe 0.     Contains information of the
  ys/Journey/Segments/Segment/ .n     SegmentInfo.
  SegmentInfo                         

  <*@id>\*                     1  Int Unique identifier of the SegmentInfo.
                                  ege 
                                  r   

  <*@transportationId>\*       1  Str Unique Id of the transportation.
                                  ing 

  <*@transportationType>\*     1  Str Transport type: F ( Flight ), T (
                                  ing Train ), B ( Bus ) & F ( Ferry ).

  <*@operatinCarrier>\*        1  Str Company which operates the
                                  ing transportation.

  <*@marketingCarrier>\*       1  Str Company which commercializes the
                                  ing transportation.

  <*@departureTerminal>\*      1  Str Departure terminal.
                                  ing 

  <*@arrivalTerminal>\*        1  Str Arrival terminal.
                                  ing 

  <*@departureDate>\*          1  Dat Departure date.
                                  e   

  <*@arrivalDate>\*            1  Dat Arrival date.
                                  e   

  <*@segmentDuration>\*        1  Int Transport duration ( in minutes ).
                                  ege 
                                  r   

  <*@maxCheckinDate>\*         1  Str Maximum date to make the check-in.
                                  ing 

  <*@segmentStatus>\*          1  Str SegmentInfo status: HK (OK), TK
                                  ing (Change of programming), UC
                                      (Unconfirmed), UN( Unable), NO (No
                                      action taken) & UD (Undefined)

  <*@hasTechnicalStop>\*       1  Boo If true, the SegmentInfo has a
                                  lea technical stop.
                                  n   

  Itineraries/Itinerary/Journe 1      Origin location.
  ys/Journey/Segments/Segment/        
  SegmentInfo/OriginLoc               

  <*@type>\*                   1  Str Type of station of the location
                                  ing indicated with A ( AirPort ), T (
                                      Train Station ) & P ( Port ).

  <*@code>\*                   1  Str Location code.
                                  ing 

  <*@cityCode>\*               1  Boo If true, the field code indicates a
                                  lea city code, if false, it will indicate
                                  n   an airport code.

  Itineraries/Itinerary/Journe 1      Destination location.
  ys/Journey/Segments/Segment/        
  SegmentInfo/DestinationLoc          

  <*@type>\*                   1  Str Type of station of the location
                                  ing indicated with A ( AirPort ), T (
                                      Train Station ) & P ( Port ).

  <*@code>\*                   1  Str Location code.
                                  ing 

  <*@cityCode>\*               1  Boo If true, the field code indicates a
                                  lea city code, if false, it will indicate
                                  n   an airport code.

  Itineraries/Itinerary/Journe 0.     Contains a list of SegmentClasses.
  ys/Journey/Segments/Segment/ .1     
  SegmentClasses                      

  Itineraries/Itinerary/Journe 0.     Contains details of the SegmentClass.
  ys/Journey/Segments/Segment/ .n     
  SegmentClasses/SegmentClass         

  <*@cabinClass>\*             1  Str Cabin class of the seat: N (Not
                                  ing specified), Y (Tourist), C
                                      (Business), F (First), CA (Cabin,
                                      only for ferries), YP (Tourist Plus)

  <*@class>\*                  1  Str Fare class.
                                  ing 

  <*@paxRef>\*                 1  Int Reference for the passenger which is
                                  ege using this fare in the transport.
                                  r   

  <*@fareBasis>\*              1  Str Fare basis.
                                  ing 

  <*@fareType>\*               1  Str Fare type: PUB ( Public ), PRI (
                                  ing Private ), NEGO ( Negotiated ) & CORP
                                      ( Corporate ).

  Itineraries/Itinerary/Journe 0.     Contains specific attributes of each
  ys/Journey/Segments/Segment/ .1     provider.
  ReservationToken                    

  Itineraries/Itinerary/Journe 0.     Contains details of the attribute.
  ys/Journey/Segments/Segment/ .n     
  ReservationToken/Attribute          

  <*@key>\*                    1  Str Keyword or id to identify a
                                  ing parameter.

  <*@value>\*                  1  Str Value of the parameter.
                                  ing 

  Itineraries/Itinerary/Amount 1      Contains details of the
  Breakdown                           AmountBreakdown.

  <*@currency>\*               1  Str Currency code of the fare.
                                  ing 

  <*@totalAmount>\*            1  Dec Total amount. with taxes and other
                                  ima charges included.
                                  l   

  <*@notCommissionableAmount>\ 1  Dec Total amount that can not be
  *                               ima commissioned.
                                  l   

  <*@commission>\*             1  Dec Commission percentage. A -1 value
                                  ima will be returned if the provider
                                  l   doesn't return any comission
                                      information.

  Itineraries/Itinerary/Amount 0.     Contains a list of ChargeBreakdowns.
  Breakdown/ChargeBreakdowns   .1     

  Itineraries/Itinerary/Amount 1.     Contains details of the
  Breakdown/ChargeBreakdowns/C .n     ChargeBreakdown.
  hargeBreakdown                      

  <*@type>\*                   1  Str ChargeBreakdown type.
                                  ing 

  <*@amount>\*                 1  Dec Total amount, with taxes included,
                                  ima associated to the passenger.
                                  l   

  Itineraries/Itinerary/Amount 1      Charge concept.
  Breakdown/ChargeBreakdowns/C        
  hargeBreakdown/Concept              

  <*@id>\*                     1  Str Indicates if the conditions are of
                                  ing one way ( with a 0 ) or round trip (
                                      with a 1 ). Ferries parameter.

  <*@language>\*               1  Str Language.
                                  ing 

  Itineraries/Itinerary/Amount 1  Str Remarks.
  Breakdown/ChargeBreakdowns/C    ing 
  hargeBreakdown/Concept/Text         

  Itineraries/Itinerary/Amount 0.     Contains a list of breakdown amounts
  Breakdown/PaxBreakdowns      .1     for each passenger ( ADT amount, etc.
                                      ).

  Itineraries/Itinerary/Amount 0.     Contains details of breakdown amounts
  Breakdown/PaxBreakdowns/PaxB .n     for each passenger.
  reakdown                            

  <*@paxType>\*                1  Str Passenger type: ADT ( Adult ), CHD (
                                  ing Child ) & INF ( Infant ).

  <*@amount>\*                 1  Dec Total amount, with taxes included,
                                  ima associated to the passenger.
                                  l   

  <*@taxes>\*                  1  Int If they exist, taxes are applied for
                                  ege this passenger type.
                                  r   

  <*@tasaDU>\*                 1  Int Deprecated
                                  ege 
                                  r   

  Itineraries/Itinerary/PaxCon 1      Contains a list of PaxConfigurations.
  figurations                         

  Itineraries/Itinerary/PaxCon 1      Contains details of the
  figurations/PaxConfiguration        PaxConfiguration.

  <*@id>\*                     1  Int Unique identifier of the
                                  ege PaxConfiguration.
                                  r   

  <*@paxRef>\*                 1  Int Reference to the passenger Id from
                                  ege the request.
                                  r   

  <*@age>\*                    1  Int Age of the passenger.
                                  ege 
                                  r   

  <*@paxType>\*                1  Str Passenger type based on the age of
                                  ing the passenger: ADT (Adult), CHD
                                      (Child), INF (Infant), YOU (Young)
                                      and SEN (Senior).

  Itineraries/Itinerary/PaxCon 0.     Applied discounts.
  figurations/PaxConfiguration .1     
  /AppliedBonuses                     

  <*@resident>\*               1  Str Resident discount type: N(None),
                                  ing BP(Balearic Islands resident flying
                                      to mainland), BI(Balearic Islands
                                      resident flying to another balearic
                                      island), DC(Canarian Islands resident
                                      flying to another Canarian Island),
                                      RC(Canarian Islands resident flying
                                      to mainland),RM(Ceuta/Melilla
                                      resident), STR(Italian resident
                                      discount), ELB(Italian resident
                                      Elba), SDG(Italian resident
                                      Sardegna), SCL(Italian resident
                                      Sicily)

  <*@largeFamily>\*            1  Str Family discount type: N(None),
                                  ing F1(Large family), F2 (Special large
                                      family).

  <*@discountCard>\*           1  Str Discount card type (for more details,
                                  ing see information below).

  Itineraries/Itinerary/PaxCon 0.     Contains a list of PaxTypeCodes.
  figurations/PaxConfiguration .1     
  /AppliedBonuses/PaxTypeCodes        

  Itineraries/Itinerary/PaxCon 0.     Contains details of the PTC.
  figurations/PaxConfiguration .n     
  /AppliebBonuses/PaxTypeCodes        
  /PaxTypeCode                        

  <*@code>\*                   1  Str String with the PTC code.
                                  ing 

  Vehicles                     0.     List of Vehicle.
                               .1     

  Vehicles/Vehicle             1.     Contains the information of the
                               .2     vehicle.

  <*@name>\*                   0. Str Name of the vehicle type.
                               .1 ing 

  <*@licensePlate>\*           1  Str License plate of the vehicle.
                                  ing 

  <*@brand>\*                  1  Str Brand name of the vehicle.
                                  ing 

  <*@model>\*                  1  Str Model of the vehicle.
                                  ing 

  <*@code>\*                   1  Str Code of the vehicle returned by the
                                  ing provider in the previous steps.

  <*@height>\*                 1  Int Height of the vehicle.
                                  ege 
                                  r   

  <*@length>\*                 1  Int Length of the vehicle.
                                  ege 
                                  r   

  <*@type>\*                   1      Vehicle type: N (None/Unknown),
                                      Tourism, 4x4, MPV, MotorbikeMax50
                                      (motorbike with less than 50 cc),
                                      MotorbikeMin50Max250 (motorbike with
                                      50 - 250 cc), MotorbikeMin250Max500
                                      (motorbike with 250 - 500 cc),
                                      MotorbikeMin500 (motorbike with more
                                      than 500 cc), Bicicle, Van,
                                      LongVehicleMax6 (vehicle larger than
                                      6 meters), Emission0Vehicle (vehicle
                                      with no emissions), Caravan, Trailer.

  Client                       1      Contains client's information.

  <*@passengerType>\*          1  Str Treatment.
                                  ing 

  <*@name>\*                   1  Str Name.
                                  ing 

  <*@surname>\*                1  Str SurName.
                                  ing 

  <*@eMail>\*                  1  Str eMail address.
                                  ing 

  <*@countryPrefix>\*          1  Str Country telephone prefix.
                                  ing 

  <*@telephone>\*              1  Str Telephone.
                                  ing 

  <*@mobilephone>\*            1  Str mobilephone Telephone.
                                  ing 

  Client/Address               1      Contains the client's address.

  <*@zipCode>\*                1  Str Zip code.
                                  ing 

  <*@countryCode>\*            1  Str Country code.
                                  ing 

  Client/Address/Street        1  Str Contains the street name of the
                                  ing address.

  Locators                     1      Contains a list of locators.

  Locators/Locator             1      Contains details of the locator.

  Locators/Locator/Id          1  Str Unique identifier of the locator.
                                  ing 

  Locators/Locator/Type        1  Str Locator type: PROVIDER,
                                  ing TFBOOKINGREFERENCE, UNIVERSAL,
                                      EMISSION and CARRIER.

  deltaPrice                   1  Dec Maximum amount increasement allowed
                                  ima between "Valoracion" and "Reserva"
                                  l   
  -------------------------------------------------------------------------

|

ReservationRS ---------

:

    <ReservationRS>
    <Locators>
        <Id>BFRFKVM</Id>
        <Type>PROVEEDOR</Type>
    </Locators>
    <Invoice carrier = "BAL" installmentsNum = "0" lastTicketingDateUTC = "0001-01-01T00:00:00">
        <AmountBreakdown currency = "EUR" totalAmount = "420" nonCommissionableAmount = "0" commission = "0.942857142857136">
            <ChargeBreakdowns>
                <ChargeBreakdown type = "VEHICLE" amount = "269.0" currency = "EUR">
                    <Concept id = "0" language = "ES">
                        <Texto>PRECIO VEHICULO</Texto>
                    </Concept>
                </ChargeBreakdown>
                <ChargeBreakdown type = "VEHICLE_FEE" amount = "11" currency = "EUR">
                    <Concept id = "1" language = "ES">
                        <Text>FEE VEHICULO</Text>
                    </Concept>
                </ChargeBreakdown>
            </ChargeBreakdowns>
            <PaxBreakdowns>
                <PaxBreakdown paxType = "ADT" amount = "140" taxes = "11" currency = "EUR"/>
            </PaxBreakdowns>
        </AmountBreakdown>
    </Invoice>

\</ReservationRS\>

|

ReservationRS Description ---------------------

  -------------------------------------------------------------------------
  Element                      Nu Typ Description
                               mb e   
                               er     
  ---------------------------- -- --- -------------------------------------
  ReservationRS                1      Root node

  Locator                      0.     List of locators given by the
                               .n     provider.

  Locators/Locator/Id          1  Str Unique identifier of the locator.
                                  ing 

  Locators/Locator/Type        1  Str Locator type: PROVIDER,
                                  ing TFBOOKINGREFERENCE, UNIVERSAL,
                                      EMISSION and CARRIER.

  Passengers                   1      Contains a list of Passengers.

  Passengers/Passenger         1.     Contains information of the
                               .n     Passenger.

  <*@passengerType>\*          1  Str Treatment: MR, MRS, CHD and INF.
                                  ing 

  <*@name>\*                   1  Str Name of the Passenger.
                                  ing 

  <*@surname>\*                1  Str Surname/s of the Passenger.
                                  ing 

  <*@bithDate>\*               1  Str Date of birth.
                                  ing 

  <*@codeDCO>\*                1  Str Document code.
                                  ing 

  <*@documentType>\*           1  Str Documentation type.
                                  ing 

  <*@documentId>\*             1  Str Unique identifier of the
                                  ing documentation.

  <*@documentExpiration>\*     1  Str Expiration date of the documentation.
                                  ing 

  <*@nationality>\*            1  Str Nationality.
                                  ing 

  Invoice                      1      

  Invoice/AmountBreakdown      1      

  <*@currency>\*               1  Str Currency code of the fare.
                                  ing 

  <*@totalAmount>\*            1  Dec Total amount. with taxes and other
                                  ima charges included.
                                  l   

  <*@notCommissionableAmount>\ 1  Dec Total amount that can not be
  *                               ima commissioned.
                                  l   

  <*@commission>\*             1  Dec Commission percentage. A -1 value
                                  ima will be returned if the provider
                                  l   doesn't return any comission
                                      information.

  Invoice/AmountBreakdown/Char 0.     Contains a list of ChargeBreakdowns.
  geBreakdowns                 .1     

  Invoice/AmountBreakdown/PaxB 0.     Contains a list of breakdown amounts
  reakdowns                    .1     for each Passenger ( ADT amount, etc.
                                      ).

  Invoice/AmountBreakdown/PaxB 0.     Contains details of breakdown amounts
  reakdowns/PaxBreakdown       .n     for each Passenger.

  <*@paxType>\*                1  Str Passenger type: ADT ( Adult ), CHD (
                                  ing Child ) & INF ( Infant ).

  <*@amount>\*                 1  Dec Total amount, with taxes included,
                                  ima associated to the Passenger.
                                  l   

  <*@taxes>\*                  1  Int If they exist, taxes are applied for
                                  ege this Passenger type.
                                  r   
  -------------------------------------------------------------------------

|