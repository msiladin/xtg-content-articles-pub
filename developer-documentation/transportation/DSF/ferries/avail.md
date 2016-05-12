---
title: Availability
keywords: transportation, data structure, ferries, availability
sidebar: mydoc_sidebar
permalink: /developer-documentation/transportation/DSF/ferries/avail
---

|

Method Goals
============

This method aims to complete the common side of the petition with the
ferries specifications, if any, and therefore have the complete petition
for ferries.

|

Request Format
==============

The request needs a list of journeys (each one with the desired dates
and ports), a list of the passengers and an optional vehicle list.

|

Response Format
===============

The response contains a list of fares with the available options.

|

AvailabilityRQ
==============

    <AvailabilityRQ xmlns:xsd = "http://www.w3.org/2001/XMLSchema" xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" travelType = "RT">
        <Journeys>
            <Journey id = "0" departureDate = "27/08/2015" departureTime = "">
                <OriginLoc type = "A" code = "PAL" citycode = "false"/>
                <DestinationLoc type = "A" code = "VAL" citycode = "false"/>
            </Journey>
            <Journey id = "1" departureDate = "04/09/2015" departureTime = "">
                <OriginLoc type = "A" code = "VAL" citycode = "false"/>
                <DestinationLoc type = "A" code  = "PAL" citycode = "false"/>
            </Journey>
        </Journeys>
        <Passengers>
            <Passenger id = "0" age = "30">
                <Bonuses resident = "N" largeFamily = "N" discountCard = "N"/>
            </Passenger>
        </Passengers>
        <Vehicles>
            <AvailabilityVehicle id = "1" height = "160" length = "350" type = "Tourism"/>
        </Vehicles>
    </AvailabilityRQ>

|

AvailabilityRQ Description
==========================

  -------------------------------------------------------------------------
  Element                          Nu Ty Description
                                   mb pe 
                                   er    
  -------------------------------- -- -- ----------------------------------
  AvailabilityRQ                   1     Root node.

  Journeys                         1     Contains a list of Journeys.

  Journeys/Journey                 1.    Contains the information about the
                                   .n    requested Journey in the
                                         availability.

  <*@id>\*                         1  In Unique identifier of the Journey.
                                      te 
                                      ge 
                                      r  

  <*@departureDate>\*              1  St Departure date.
                                      ri 
                                      ng 

  <*@departureTime>\*              1  St Departure time.
                                      ri 
                                      ng 

  Journeys/Journey/OriginLoc       1     Origin location.

  <*@type>\*                       1  St Type of station of the location
                                      ri indicated with A ( AirPort ), T (
                                      ng Train Station ) & P ( Port ).

  <*@code>\*                       1  St Location code.
                                      ri 
                                      ng 

  <*@cityCode>\*                   1  Bo If true, the field code indicates
                                      ol a city code, if false, it will
                                      ea indicate an airport code.
                                      n  

  Journeys/Journey/DestinationLoc  1     Destination location.

  <*@type>\*                       1  St Type of station of the location
                                      ri indicated with A ( AirPort ), T (
                                      ng Train Station ) & P ( Port ).

  <*@code>\*                       1  St Location code.
                                      ri 
                                      ng 

  <*@cityCode>\*                   1  Bo If true, the field code indicates
                                      ol a city code, if false, it will
                                      ea indicate an airport code.
                                      n  

  Passengers                       1     Contains a list of Passengers.

  Passengers/Passenger             1.    Contains information of the
                                   .n    Passenger

  <*@id>\*                         1  In Unique identifier of the
                                      te Passenger.
                                      ge 
                                      r  

  <*@age>\*                        1  In Age of the Passenger.
                                      te 
                                      ge 
                                      r  

  Passengers/Passenger/Bonuses     0.    Possible discount or bonuses.
                                   .1    

  <*@resident>\*                   1  St Resident discount.
                                      ri 
                                      ng 

  <*@largeFamily>\*                1  St Family discount.
                                      ri 
                                      ng 

  <*@discountCard>\*               1  St Discount card.
                                      ri 
                                      ng 

  Passengers/Passenger/Bonuses/Pax 0.    Contains a list of additional
  TypeCodes                        .1    passengers types.

  Passengers/Passenger/Bonuses/Pax 1.    Contains information of the
  TypeCodes/PaxTypeCode            .n    additional passenger type.

  <*@code>\*                       1  St Specific discounts by passenger
                                      ri type in a provider format.
                                      ng 

  Vehicles                         0.    Contains a list of vehicles.
                                   .1    

  AvailabilityVehicle              1.    Contains details of the vehicles.
                                   .2    

  <*@id>\*                         1     Unique identifier of the vehicle.

  <*@height>\*                     1     Dimension of the vehicle: height

  <*@length>\*                     1     Dimension of the vehicle: width

  <*@type>\*                       1     Type of vehicle:
  -------------------------------------------------------------------------

|

AvailabilityRS
==============

    <AvailabilityRS xmlns:xsd = "http://www.w3.org/2001/XMLSchema" xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance">
    <operationImplemented>true</operationImplemented>
    <EstadoRespuesta tipoTrayecto = "IDA" tipoPet = "OW" estado = "ok"/>
    <Transportation>
        <Segments>
            <Segment id = "1" transportationId = "BJ1#VISEMAR ONE#FERRY" transportationType = "F" operatingCarrier = "BAL" marketingCarrier = "BAL" departureTerminal = "PAL" arrivalTerminal = "VAL" departureDate = "2015-08-27T11:30:00" arrivalDate = "2015-08-27T19:30:00"  transportationName = "VISEMAR ONE" transportationCode = "BJ1" segmentStatus = "HK"  tieneParadaTecnica = "false">
                <OriginLoc type = "P" code = "PAL" citycode = "false"/>
                <DestinationLoc type = "P" code = "VAL" citycode = "false"/>
            </Segment>
            <Segment id = "2" transportationId = "BJ1#VISEMAR ONE#FERRY" transportationType = "F" operatingCarrier = "BAL" marketingCarrier = "BAL" departureTerminal = "VAL" arrivalTerminal = "PAL" departureDate = "2015-09-04T22:15:00" arrivalDate = "2015-09-05T06:00:00"  transportationName = "VISEMAR ONE" transportationCode = "BJ1" segmentStatus = "HK"  tieneParadaTecnica = "false">
                <OriginLoc type = "P" code = "VAL" citycode = "false"/>
                <DestinationLoc type = "P" code = "PAL" citycode = "false"/>
            </Segment>
        </Segments>
        <Fares>
            <Fare id = "0" providerCode = "BAL" fareType = "OW">
                <Conditions>
                    <Condition id = "0" language = "ES">
                        <Text>CAFETERIA#CAFETERIA##RTN#TARIFA IDA Y VUELTA#F0-TRAYECTO SIN RESTRICCIONES#F0#2.09</Text>
                    </Condition>
                </Conditions>
                <Options>
                    <Option id = "-1" availabilityJourneyRef = "0" numStopOvers = "0">
                        <SegmentReferences>
                            <SegmentReference segmentRef = "1">
                                <SegmentClasses>
                                    <SegmentClass cabinClass = "N" class = "CAFETERIA" paxRef = "0" fareType = "PUB">
                                        <CancellationPolicies>
                                            <CancellationPolicy amount = "0" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-19T10:16:00" refundable = "true"/>
                                            <CancellationPolicy amount = "10" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-20T11:30:00" refundable = "true"/>
                                            <CancellationPolicy amount = "20" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-25T11:30:00" refundable = "true"/>
                                            <CancellationPolicy amount = "100" currency = "EUR" amountType = "PERCENTUAL" fromDate = "2015-08-27T11:30:00" refundable = "true"/>
                                        </CancellationPolicies>
                                        <Modifiable modifiable = "true" amount = "0" amountType = "AMOUNT">
                                            <Description>Admite cambios sin cargos</Description>
                                        </Modifiable>
                                    </SegmentClass>
                                </SegmentClasses>
                                <ReservationTokens/>
                            </SegmentReference>
                        </SegmentReferences>
                    </Option>
                </Options>
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
                        <PaxBreakdown paxType = "ADT" amount = "75.5" currency = "EUR" taxes = "11" />
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
            </Fare>
            <Fare id = "1" providerCode = "BAL" fareType = "OW">
                <Conditions>
                    <Condition id = "0" language = "ES">
                        <Text>C4#CAMAROTE CUADRUPLE#ACOMODACION EN CAMAROTE CUADRUPLE EXCLUSIVO Y ACCESO AL SALON NEPTUNO SUJETO A DISPONIBILIDAD#RTN#TARIFA IDA Y VUELTA#F0-TRAYECTO SIN RESTRICCIONES#F0#3.19</Text>
                    </Condition>
                </Conditions>
                <Options>
                    <Option id = "-1" availabilityJourneyRef = "0" numStopOvers = "0">
                        <SegmentReferences>
                            <SegmentReference segmentRef = "1">
                                <SegmentClasses>
                                    <SegmentClass cabinClass = "CA" class = "C4" paxRef = "0" fareType = "PUB">
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
                                <ReservationTokens/>
                            </SegmentReference>
                        </SegmentReferences>
                    </Option>
                </Options>
                <AmountBreakdown currency = "EUR" totalAmount = "331" nonCommissionableAmount = "0" commission = "0.963746223564954">
                    <ChargeBreakdowns>
                        <ChargeBreakdown type = "VEHICLE" amount = "134.5" currency = "EUR">
                            <Concept id = "0" language = "ES">
                                <Text>PRECIO VEHICULO IDA</Text>
                            </Concept>
                        </ChargeBreakdown>
                        <ChargeBreakdown type = "VEHICLE_FEE" amount = "11" currency = "EUR">
                            <Concept id = "1" language = "ES">
                                <Text>FEE VEHICULO IDA</Text>
                            </Concept>
                        </ChargeBreakdown>
                    </ChargeBreakdowns>
                    <PaxBreakdowns>
                        <PaxBreakdown paxType = "ADT" amount = "185.5" currency = "EUR" taxes = "11"/>
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
            </Fare>
            <Fare id = "2" providerCode = "BAL" fareType = "OW">
                <Conditions>
                    <Condition id = "0" language = "ES">
                        <Text>CAFETERIA#CAFETERIA##RTN#TARIFA IDA Y VUELTA#F0-TRAYECTO SIN RESTRICCIONES#F0#1.87</Text>
                    </Condition>
                </Conditions>
                <Options>
                    <Option id = "-1" availabilityJourneyRef = "1" numStopOvers = "0">
                        <SegmentReferences>
                            <SegmentReference segmentRef = "2">
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
                                <ReservationTokens/>
                            </SegmentReference>
                        </SegmentReferences>
                    </Option>
                </Options>
                <AmountBreakdown currency = "EUR" totalAmount = "199" nonCommissionableAmount = "0" commission = "0.939698492462313">
                    <ChargeBreakdowns>
                        <ChargeBreakdown type = "VEHICLE" amount = "134.5" currency = "EUR">
                            <Concept id = "0" language = "ES">
                                <Text>PRECIO VEHICULO VUELTA</Text>
                            </Concept>
                        </ChargeBreakdown>
                    </ChargeBreakdowns>
                    <PaxBreakdowns>
                        <PaxBreakdown paxType = "ADT" amount = "64.5" currency = "EUR" taxes = "0" />
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
            </Fare>
            <Fare id = "3" providerCode = "BAL" fareType = "OW">
                <Conditions>
                    <Condition id = "0" language = "ES">
                        <Text>C4#CAMAROTE CUADRUPLE#ACOMODACION EN CAMAROTE CUADRUPLE EXCLUSIVO Y ACCESO AL SALON NEPTUNO SUJETO A DISPONIBILIDAD#RTN#TARIFA IDA Y VUELTA#F0-TRAYECTO SIN RESTRICCIONES#F0#2.97</Text>
                    </Condition>
                </Conditions>
                <Options>
                    <Option id = "-1" availabilityJourneyRef = "1" numStopOvers = "0">
                        <SegmentReferences>
                            <SegmentReference segmentRef = "2">
                                <SegmentClasses>
                                    <SegmentClass cabinClass = "CA" class = "C4" paxRef = "0" fareType = "PUB">
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
                                <ReservationTokens/>
                            </SegmentReference>
                        </SegmentReferences>
                    </Option>
                </Options>
                <AmountBreakdown currency = "EUR" totalAmount = "309" nonCommissionableAmount = "0" commission = "0.961165048543705">
                    <ChargeBreakdowns>
                        <ChargeBreakdown type = "VEHICLE" amount = "134.5" currency = "EUR">
                            <Concept id = "0" language = "ES">
                                <Text>PRECIO VEHICULO VUELTA</Text>
                            </Concept>
                        </ChargeBreakdown>
                    </ChargeBreakdowns>
                    <PaxBreakdowns>
                        <PaxBreakdown paxType = "ADT" amount = "174.5" currency = "EUR" taxes = "0" />
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
            </Fare>           
        </Fares>
    </Transportation>

\</AvailabilityRS\>

|

AvailabilityRS Description
==========================

  -------------------------------------------------------------------------
  Element                      Nu Typ Description
                               mb e   
                               er     
  ---------------------------- -- --- -------------------------------------
  AvailabilityRS               1      Root node.

  Transportation               1      Contains all of the Segments and
                                      Fares.

  Transportation/Segments      1      Contains a list of the Segments.

  Transportation/Segments/Segm 1.     Contains the information of the
  ent                          .n     segment.

  <*@id>\*                     1  Int Unique identifier of the segment.
                                  ege 
                                  r   

  <*@transportationId>\*       1  Str Unique Id of the transportation.
                                  ing 

  <*@transportationType>\*     1  Str Transport type: F ( Flight ), T (
                                  ing Train ), B ( Bus ) & F ( Ferry ).

  <*@operatingCarrier>\*       1  Str Company which operates the
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

  <*@transportationName>\*     0. Str Name of the vessel.
                               .1 ing 

  <*@transportationCode>\*     0. Str Code that identifies the vessel.
                               .1 ing 

  <*@segmentStatus>\*          1  Str Segment status: HK (OK), TK (Change
                                  ing of programming), UC (Unconfirmed),
                                      UN( Unable), NO (No action taken) &
                                      UD (Undefined)

  <*@hasTechnicalStop>\*       1  Boo If true, the segment has a technical
                                  lea stop.
                                  n   

  Transportation/Segments/Segm 1      Origin location.
  ent/OriginLoc                       

  <*@type>\*                   1  Str Type of station of the location
                                  ing indicated with A ( AirPort ), T (
                                      Train Station ) & P ( Port ).

  <*@code>\*                   1  Str Location code.
                                  ing 

  <*@cityCode>\*               1  Boo If true, the field code indicates a
                                  lea city code, if false, it will indicate
                                  n   an airport code.

  Transportation/Segments/Segm 1      Destination location.
  ent/DestinationLoc                  

  <*@type>\*                   1  Str Type of station of the location
                                  ing indicated with A ( AirPort ), T (
                                      Train Station ) & P ( Port ).

  <*@code>\*                   1  Str Location code.
                                  ing 

  <*@cityCode>\*               1  Boo If true, the field code indicates a
                                  lea city code, if false, it will indicate
                                  n   an airport code.

  Transportation/Segments/Segm 0.     Contains a list of TechnicalStops.
  ent/TechnicalStops           .1     

  <*@totalTechnicalStops>\*    1  Int Total number of TechnicalStops.
                                  ege 
                                  r   

  Transportation/Segments/Segm 1.     Contains the details of the
  ent/TechnicalStops/Technical .n     TechnicalStop.
  Stop                                

  <*@location>\*               1  Str TechnicalStop location.
                                  ing 

  <*@stopDate>\*               1  Dat Approx. stop date and time.
                                  e   

  <*@departureDate>\*          1  Dat Approx. departure date and time.
                                  e   

  Fares                        1      Contains a list of Fares.

  Fares/Fare                   1.     Contains details of Fare.
                               .n     

  <*@id>\*                     1  Int Unique identifier of the Fare.
                                  ege 
                                  r   

  <*@providerCode>\*           1  Str Code of the provider that offers this
                                  ing fare.

  <*@fareType>\*               1  Str Fare type: OW ( one way ), RT ( round
                                  ing trip ), OJ ( Open jaw ) & CT ( Circle
                                      trip ).

  Fares/Fare/Conditions        1      Contains a list of Fare Conditions.

  Fares/Fare/Conditions/Condit 1.     Contains details of the Fare
  ion                          .n     Condition.

  <*@id>\*                     1  Str Indicates if the conditions are of
                                  ing one way ( with a 0 ) or round trip (
                                      with a 1 ). Ferries parameter.

  <*@language>\*               1  Str Language.
                                  ing 

  Fares/Fare/Conditions/Condit 1  Str In Ferries it contains the following:
  ion/Text                        ing "AccomodationCode\#AccomodationName\#
                                      AccomodationDescription\#FareCode\#Fa
                                      reName\#FareDescription".

  Fares/Fare/Options           1      Contains a list of Fare Options.

  Fares/Fare/Options/Option    1.     Contains details of the Fare Options.
                               .n     

  <*@id>\*                     1  Int Deprecated attribute.
                                  ege 
                                  r   

  <*@availJourneyRef>\*        1  Int Reference number of the availability
                                  ege Journey.
                                  r   

  <*@numStopOver>\*            1  Int Number of StopOvers. If -1, then we
                                  ege cannot know how many StopOvers via
                                  r   XML.

  <*@carrier>\*                1  Str Validating carrier.
                                  ing 

  Fares/Fare/Options/Option/Se 1      Contains a list of SegmentReferences.
  gmentReferences                     

  Fares/Fare/Options/Option/Se 1.     Contains details of the
  gmentReferences/SegmentRefer .n     SegmentReference of each option.
  ence                                

  <*@segmentRef>\*             1  Int Reference of the Segment.
                                  ege 
                                  r   

  Fares/Fare/Options/Option/Se 1      Contains a list of SegmentClasses.
  gmentReferences/SegmentRefer        
  ence/SegmentClasses                 

  Fares/Fare/Options/Option/Se 1      Contains details of the SegmentClass.
  gmentReferences/SegmentRefer ..     
  ence/SegmentClasses/SegmentC n      
  lass                                

  <*@cabinClass>\*             1  Str Cabin class of the seat: N (Not
                                  ing specified), Y (Tourist), C
                                      (Business), F (First), CA (Cabin,
                                      only for ferries), YP (Tourist Plus)

  <*@class>\*                  1  Str Fare class. In ferries indicates the
                                  ing accomodation code.

  <*@paxRef>\*                 1  Int Passenger reference.
                                  ege 
                                  r   

  <*@fareBasis>\*              1  Str Identifier of the fare.
                                  ing 

  <*@fareType>\*               1  Str Fare type: PUB ( Public ), PRI (
                                  ing Private ), NEGO ( Negotiated ) and
                                      CORP ( Corporate ).

  <*@avail>\*                  1  Int Available seats remaining for this
                                  ege class (In flights, the maximum is 9)
                                  r   

  Fares/Fare/Options/Option/Se 0.     Specific attribute used for each
  gmentReferences/SegmentRefer .1     provider.
  ence/ReservationTokens              

  Fares/Fare/Options/Option/Se 0.     Type of attribute.
  gmentReferences/SegmentRefer .n     
  ence/ReservationTokens/Attri        
  bute                                

  <*@key>\*                    1  Str Contains the keyword/ Id to identify
                                  ing a parameter.

  <*@value>\*                  1  Str Contains the value of the parameter.
                                  ing 

  Fares/Fare/AmountBreakdown   1      Breakdown of the fare amount.

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

  Fares/Fare/AmountBreakdown/C 0.     Contains a list of breakdown amounts
  hargeBreakdowns              .1     ( taxes, mandatory charges.. ).

  Fares/Fare/AmountBreakdown/C 1.     Contains details of the
  hargeBreakdowns/ChargeBreakd .n     BreakdownAmount.
  own                                 

  <*@type>\*                   1  Str Charge type.
                                  ing 

  <*@amount>\*                 1      Charge amount.

  Fares/Fare/AmountBreakdown/C 0.     Contains a list of breakdown amounts
  hargeBreakdowns/ChargeBreakd .1     ( taxes, mandatory charges.. ).
  own/Concept                         

  <*@id>\*                     1  Str Indicates if the conditions are of
                                  ing one way ( with a 0 ) or round trip (
                                      with a 1 ). Ferries parameter.

  <*@language>\*               1  Str Language.
                                  ing 

  Fares/Fare/AmountBreakdown/C 1  Str Remarks.
  hargeBreakDowns/ChargeBreakd    ing 
  own/Concept/Text                    

  Fares/Fare/AmountBreakdown/P 0.     Contains a list of breakdown amounts
  axBreakdown                  .1     for each passenger ( ADT amount, etc.
                                      ).

  Fares/Fare/AmountBreakdown/P 0.     Contains details of breakdown amounts
  axBreakdowns/PaxBreakdown    .n     for each passenger.

  <*@paxType>\*                1  Str Passenger type: ADT ( Adult ), CHD (
                                  ing Child ) & INF ( Infant ).

  <*@amount>\*                 1  Dec Total amount, with taxes included,
                                  ima associated to the passenger.
                                  l   

  <*@taxes>\*                  1  Int If they exist, taxes are applied for
                                  ege this passenger type.
                                  r   

  Fares/Fare/PaxConfigurations 1      Contains a list of PaxConfiguration.

  Fares/Fare/PaxConfigurations 1.     Contains details of PaxConfiguration.
  /PaxConfiguration            .n     

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