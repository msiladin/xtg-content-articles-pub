---
title: Valuation
keywords: transportation, data structure, ferries, valuation
sidebar: mydoc_sidebar
permalink: /developer-documentation/transportation/DSF/ferries/valuation
---

|

Method Goals
============

This method aims to do a prebook of the selected Option. This Option
**must** be selected in the previous step ( Availability ).

The Valuation request must be built from results of a single
Availability. Mixing OneWay options from different Availability calls do
not grant the correct functionability of the Valuation.

|

Request Format
==============

The Valuation request can be done by two different ways: with a single
Itinerary or multiple Itineraries.

-   Multiple Itineraries :

In this method, the request will have as many Itineraries as there are
Journeys . Mainly used for **one-way** tickets. There's a total price
for each selected SegmentInfo.

-   Single Itinerary with one or more Journeys :

This case is used for **round trip** tickets. There's only one
**totalAmount** (fare, tax and discount) for all the selected Journey .

The decision of which strategy to take is done beforehand, depending on
the business rules.

|

Response Format
===============

The returned XML is very similar to the result in the Availability call.
The main difference is that there is only one node Option returned. The
totalAmount is definitive. Sometimes this method will fail since the
selected Option at Availability may not be available for this stage. In
this case the integration returns an error code 301 ( link missing ).

|

Remarks
=======

Some suppliers do not provide this method. If this is the case then all
of the information **must** be returned in the Availability, therefore
the Valuation call will do the Availability process again filtered by
the selected Option.

|

ValuationRQ Example
===================

    <ValuationRQ>
    <Itineraries>
        <Itinerary id = "0">
            <Conditions>
                <Condition id = "0" language = "ES">
                    <Text>CAFETERIA#CAFETERIA##RTN#TARIFA IDA Y VUELTA#F0-TRAYECTO SIN RESTRICCIONES#F0#2.09</Text>
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
            </Journeys>
            <AmountBreakdown currency = "EUR" totalAmount = "221" nonCommissionableAmount = "0" commission = "0.945701357466064">
                <ChargeBreakdowns>
                    <ChargeBreakdown type = "VEHICLE" amount = "134.5" currency = "EUR">
                        <Concept id = "0" language = "ES">
                            <Texto>PRECIO VEHICULO IDA</Texto>
                        </Concept>
                    </ChargeBreakdown>
                    <ChargeBreakdown type = "VEHICLE_FEE" amount = "11" currency = "EUR">
                        <Concept id = "1" language = "ES">
                            <Text>FEE VEHICULO IDA</Text>
                        </Concept>
                    </ChargeBreakdown>
                </ChargeBreakdowns>
                <PaxBreakdowns>
                    <PaxBreakdown paxType = "ADT" amount = "75.5" currency = "EUR" taxes = "11"/>
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
        <Itinerary id = "0">
            <Conditions>
                <Condition id = "0" language = "ES">
                    <Text>CAFETERIA#CAFETERIA##RTN#TARIFA IDA Y VUELTA#F0-TRAYECTO SIN RESTRICCIONES#F0#1.87</Text>
                </Condition>
            </Conditions>
            <Journeys>
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
                            <TokensReserva/>
                        </Segment>
                    </Segments>
                </Journey>
            </Journeys>
            <AmountBreakdown currency = "EUR" totalAmount = "199" nonCommissionableAmount = "0" commission = "0.939698492462313">
                <ChargeBreakdowns>
                    <ChargeBreakdown type = "VEHICLE" amount = "134.5">
                        <Concept id = "0" language = "ES">
                            <Text>PRECIO VEHICULO VUELTA</Text>
                        </Concept>
                    </ChargeBreakdown>
                </ChargeBreakdowns>
                <PaxBreakdowns>
                    <PaxBreakdown paxType = "ADT" amount = "64.5" taxes = "0"/>
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

\</ValuationRQ\>

|

ValuationRQ Description
=======================

  -------------------------------------------------------------------------
  Element                      Nu Typ Description
                               mb e   
                               er     
  ---------------------------- -- --- -------------------------------------
  ValuationRQ                  1      Root node.

  <*@specialSupplments>\*      1  Boo Special supplements.
                                  lea 
                                  n   

  <*@extendedFareRules>\*      1  Boo Extended Fare Rules.
                                  lea 
                                  n   

  <*@seating>\*                1  Boo Map of available seats.
                                  lea 
                                  n   

  Itineraries                  1      List of Itineraries.

  Itineraries/Itinerary        1.     Details of the Itinerary.
                               .n     

  <*@id>\*                     1  Int Unique identifier of the Itinerary.
                                  ege 
                                  r   

  <*@fareRef>\*                1  Int Reference identifier to the original
                                  ege Fare. Flights parameter.
                                  r   

  <*@HasObFees>\*              1  Boo If true then there is an extra fee
                                  lea for using credit card.
                                  n   

  <*@carrier>\*                1  Str Validating carrier. Flights
                                  ing parameter.

  Itineraries/Itinerary/Condit 0.     Contains a list of Conditions.
  ions                         .1     

  Itineraries/Itinerary/Condit 0.     Contains details of the Condition.
  ions/Condition               .n     

  <*@id>\*                     1  Str Indicates if the conditions are of
                                  ing one way ( with a 0 ) or round trip (
                                      with a 1 ). Ferries parameter.

  <*@language>\*               1  Str Language.
                                  ing 

  Itineraries/Itinerary/Condit 1  Str Remarks.
  ions/Condition/Text             ing 

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

  <*@planeType>\*              1  Str Plane type. Flights parameter.
                                  ing 

  <*@maxCheckinDate>\*         1  Str Maximum date to make the check-in.
                                  ing 

  <*@segmentStatus>\*          1  Str SegmentInfo status: HK (OK), TK
                                  ing (Change of programming), UC
                                      (Unconfirmed), UN( Unable), NO (No
                                      action taken) & UD (Undefined)

  <*@hasTechnicalStop>\*       1  Boo If true, the SegmentInfo has a
                                  lea technical stop.
                                  n   

  <*@electronicTicket>\*       1  Boo If true, the SegmentInfo uses a
                                  lea electronic ticket.
                                  n   

  <*@secureFlight>\*           0. Boo If true, the provider requires extra
                               .1 lea information of the passengers.
                                  n   Flights parameter.

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

  <*@avail>\*                  1  Int Available seats remaining for this
                                  ege class (In flights, the maximum is 9)
                                  r   

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

  Fares/Fare/PaxConfigurations 0.     Applied discounts.
  /PaxConfiguration/AppliedBon .1     
  uses                                

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

  Fares/Fare/PaxConfigurations 0.     Contains a list of PaxTypeCodes.
  /PaxConfiguration/AppliedBon .1     
  uses/PaxTypeCodes                   

  Fares/Fare/PaxConfigurations 0.     Contains details of the PTC.
  /PaxConfiguration/AppliedBon .n     
  uses/PaxTypeCodes/PaxTypeCod        
  e                                   

  <*@code>\*                   1  Str String with the PTC code.
                                  ing 

  Fares/Fare/VehicleConfigurat 0.     Contains a list of
  ions                         .1     VehicleConfiguration.

  Fares/Fare/VehicleConfigurat 1.     Contains details of
  ions/VehicleConfiguration    .2     VehicleConfiguration.

  <*@vehicleRef>\*             1  Str References the vehicle id of the
                                  ing request.

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

  <*@code>\*                   1  Str The code that identifies this type of
                                  ing vehicle in the providers system.

  <*@name>\*                   0. Str Name of the vehicle type
                               .1 ing 
  -------------------------------------------------------------------------

|

ValuationRS Example
===================

    <ValuationRS>
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
                            <TokensReserva/>
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

\</ValuationRS\>

|

ValuationRS Description
=======================

  -------------------------------------------------------------------------
  Element                      Nu Typ Description
                               mb e   
                               er     
  ---------------------------- -- --- -------------------------------------
  ValuationRS                  1      Root node.

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

  Fares/Fare/VehicleConfigurat 0.     Contains a list of
  ions                         .1     VehicleConfiguration.

  Fares/Fare/VehicleConfigurat 1.     Contains details of
  ions/VehicleConfiguration    .2     VehicleConfiguration.

  <*@vehicleRef>\*             1  Str References the vehicle id of the
                                  ing request.

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

  <*@code>\*                   1  Str The code that identifies this type of
                                  ing vehicle in the providers system.

  <*@name>\*                   0. Str Name of the vehicle type
                               .1 ing 
  -------------------------------------------------------------------------