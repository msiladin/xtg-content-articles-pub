---
title: Valuation
keywords: transportation, data structure, flights, valuation
sidebar: mydoc_sidebar
permalink: /developer-documentation/transportation/DSF/flights/valuation
---

|

Method Goals
============

This method aims to return the total price of the selected Option. This
Option **must** be selected in the previous step ( Availability ).

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

ValoracionRQ Example
====================

    <ValuationRQ>
        <ClientConfiguration currencyCode = "EUR"/>
        <Itineraries>
            <Itinerary id="0" carrier = "UX">
                 <Conditions>
                     <Condition id="1" language="en"/>
                 </Conditions>
                <Journeys>
                    <Journey id="0">
                        <Segments>
                            <Segment id="0">
                                <SegmentInfo transportationId = "0B104" transportationType = "V" operatingCarrier = "0B" marketingCarrier = "0B" departureDate = "2014-03-23T10:20:00" arrivalDate = "2014-03-23T15:15:00" planeType = "734" segmentStatus = "HK" electronicTicket = "true" hasTechnicalStop = "false">
                                    <OriginLoc type = "A" code = "MAD" cityCode = "false"/>
                                    <DestinationLoc type = "A" code = "OTP" cityCode = "false"/>
                                </SegmentInfo>
                                <SegmentClasses>
                                    <SegmentClass cabinClass = "Y" class = "K" paxRef = "0" fareBasis = "WEB14" fareType = "PUB"/>
                                </SegmentClasses>
                                <ReservationTokens>
                                    <Attribute key = "FareSequence" value = "88"/>
                                    <Attribute key = "RuleNumber" value = "0001"/>
                                </ReservationTokens>
                            </Segment>
                        </Segments>
                    </Journey>
                </Journeys>
                <ChargeBreakdown currency = "EUR" totalAmount = "109.9000">
                    <ChargeBreakdowns/>
                    <PaxBreakdowns>
                        <PaxBreakdown paxType = "ADT" amount = "109.9000"/>
                    </PaxBreakdowns>
                </ChargeBreakdown>
                <PaxConfigurations>
                    <PaxConfiguration id = "0" paxRef = "0" age = "30" paxType = "ADT">
                        <AppliedBonuses resident = "N" largeFamily = "N" discountCard = "N"/>
                    </PaxConfiguration>
                </PaxConfigurations>
                <ConfigurationesVehiculos/>
                <Emisiones/>
            </Itinerary>
            <Itinerary id="1" carrier = "UX">
                <Journeys>
                    <Journey id="0">
                        <Segments>
                            <Segment id="0">
                                <SegmentInfo transportationId = "UX103" transportationType = "V" operatingCarrier = "0B" marketingCarrier = "0B" departureDate = "2014-03-25T15:30:00" arrivalDate = "2014-03-25T18:35:00" maxCheckinDate = "0001-01-01T00:00:00" planeType = "734" segmentStatus = "HK" electronicTicket = "true" hasTechnicalStop = "false">
                                    <OriginLoc type = "A" code = "OTP" cityCode = "false"/>
                                    <DestinationLoc type = "A" code = "MAD" cityCode = "false"/>
                                </SegmentInfo>
                                <SegmentClasses>
                                    <SegmentClass cabinClass = "Y" class = "L" paxRef = "0" fareBasis = "WEB13" fareType = "PUB"/>
                                </SegmentClasses>
                                <ReservationTokens>
                                    <Attribute key = "FareSequence" value = "88"/>
                                    <Attribute key = "RuleNumber" value = "0001"/>
                                </ReservationTokens>
                            </Segment>
                        </Segments>
                    </Journey>
                </Journeys>
                <ChargeBreakdown currency = "EUR" totalAmount = "99.9000">
                    <ChargeBreakdowns/>
                    <PaxBreakdowns>
                        <PaxBreakdown paxType = "ADT" amount = "99.9000" taxes = "0" tasaDU = "0"/>
                    </PaxBreakdowns>
                </ChargeBreakdown>
                <PaxConfigurations>
                    <PaxConfiguration id = "0" paxRef = "0" age = "30" paxType = "ADT">
                        <AppliedBonuses resident = "N" largeFamily = "N" discountCard = "N"/>
                    </PaxConfiguration>
                </PaxConfigurations>
            </Itinerary>
        </Itineraries>
    </ValuationRQ>

|

ValoracionRQ Description
========================

  -------------------------------------------------------------------------
  Element                      Nu Typ Description
                               mb e   
                               er     
  ---------------------------- -- --- -------------------------------------
  ValuationRQ                  1      Root node. |

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

  <*@commission>\*             1  Dec Commission.
                                  ima 
                                  l   

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
  -------------------------------------------------------------------------

|

ValuationRS Example
===================

    <ValuationRS>
        <Itineraries>
            <Itinerary id="0" HasObFees="false" carrier="SK">
                <Conditions>
                    <Condition id="PEN">
                        <Text>TICKETS ARE NON-REFUNDABLE</Text>
                    </Condition>
                    <Condition id="LTD">
                        <Text>LAST TKT DTE, 09JAN15, - SEE ADV PURCHASE</Text>
                    </Condition>
                </Conditions>
                <Journeys>
                    <Journey id="0" Duracion="0">
                        <Segments>
                            <Segment id="0">
                                <SegmentInfo id="0" transportationId="SK550" transportationType="V"
                                    operatingCarrier="SK" marketingCarrier="SK" arrivalTerminal="3"
                                    departureDate="2015-03-27T07:00:00" arrivalDate="2015-03-27T08:20:00"
                                    segmentDuration="0" maxCheckinDate="2015-01-09T00:00:00"
                                    planeType="320" segmentStatus="HK" electronicTicket="true"
                                    hasTechnicalStop="false" secureFlight="false">
                                    <OriginLoc type="A" code="AMS" cityCode="false"/>
                                    <DestinationLoc type="A" code="CPH" cityCode="false"/>
                                </SegmentInfo>
                                <SegmentClasses>
                                    <SegmentClass cabinClass="Y" class="O" paxRef="0"
                                        fareBasis="ONLOWM3" fareType="PUB"/>
                                    <SegmentClass cabinClass="Y" class="O" paxRef="1"
                                        fareBasis="ONLOWM3" fareType="PUB"/>
                                    <SegmentClass cabinClass="Y" class="O" paxRef="2"
                                        fareBasis="ONLOWM3" fareType="PUB"/>
                                    <SegmentClass cabinClass="Y" class="O" paxRef="3"
                                        fareBasis="ONLOWM3" fareType="PUB"/>
                                </SegmentClasses>
                                <ReservationTokens>
                                    <Attribute key="LtdProv" value="260215"/>
                                    <Attribute key="Ltd" value="26/02/2015"/>
                                    <Attribute key="cabinClass" value="N"/>
                                    <Attribute key="validatingCarrier" value="SK"/>
                                    <Attribute key="horaVal" value="2015-02-26T10:33:06.282"/>
                                </ReservationTokens>
                            </Segment>
                            <Segment id="1">
                                <SegmentInfo id="1" transportationId="SK2240" transportationType="V"
                                    operatingCarrier="SK" marketingCarrier="SK" departureTerminal="3"
                                    arrivalTerminal="3" departureDate="2015-03-27T10:25:00"
                                    arrivalDate="2015-03-27T14:15:00" segmentDuration="0"
                                    maxCheckinDate="2015-01-09T00:00:00" planeType="320"
                                    segmentStatus="HK" electronicTicket="true"
                                    hasTechnicalStop="false" secureFlight="false">
                                    <OriginLoc type="A" code="CPH" cityCode="false"/>
                                    <DestinationLoc type="A" code="AGP" cityCode="false"/>
                                </SegmentInfo>
                                <SegmentClasses>
                                    <SegmentClass cabinClass="Y" class="O" paxRef="0"
                                        fareBasis="ONLOWM3" fareType="PUB"/>
                                    <SegmentClass cabinClass="Y" class="O" paxRef="1"
                                        fareBasis="ONLOWM3" fareType="PUB"/>
                                    <SegmentClass cabinClass="Y" class="O" paxRef="2"
                                        fareBasis="ONLOWM3" fareType="PUB"/>
                                    <SegmentClass cabinClass="Y" class="O" paxRef="3"
                                        fareBasis="ONLOWM3" fareType="PUB"/>
                                </SegmentClasses>
                                <ReservationTokens>
                                    <Attribute key="LtdProv" value="260215"/>
                                    <Attribute key="Ltd" value="26/02/2015"/>
                                    <Attribute key="cabinClass" value="N"/>
                                    <Attribute key="validatingCarrier" value="SK"/>
                                    <Attribute key="horaVal" value="2015-02-26T10:33:06.282"/>
                                </ReservationTokens>
                            </Segment>
                        </Segments>
                    </Journey>
                </Journeys>
                <ChargeBreakdown currency="EUR" totalAmount="312.41" notCommissionableAmount="0"
                    commission="-1">
                    <ChargeBreakdowns/>
                    <PaxBreakdowns>
                        <PaxBreakdown paxType="ADT" amount="105.47" taxes="75.47" tasaDU="0"/>
                        <PaxBreakdown paxType="CHD" amount="98.47" taxes="75.47" tasaDU="0"/>
                        <PaxBreakdown paxType="INF" amount="3.00" taxes="0.00" tasaDU="0"/>
                    </PaxBreakdowns>
                </ChargeBreakdown>
                <PaxConfigurations>
                    <PaxConfiguration id="0" paxRef="0" age="30" paxType="ADT">
                        <AppliedBonuses resident="N" largeFamily="N" discountCard="N"/>
                        <PaxTypeCodes>
                            <PaxTypeCode code="IT"/>
                        </PaxTypeCodes>
                    </PaxConfiguration>
                    <PaxConfiguration id="1" paxRef="1" age="8" paxType="CHD">
                        <AppliedBonuses resident="N" largeFamily="N" discountCard="N"
                        />
                    </PaxConfiguration>
                    <PaxConfiguration id="2" paxRef="2" age="1" paxType="INF">
                        <AppliedBonuses resident="N" largeFamily="N" discountCard="N"
                        />
                    </PaxConfiguration>
                    <PaxConfiguration id="3" paxRef="3" age="70" paxType="ADT">
                        <AppliedBonuses resident="N" largeFamily="N" discountCard="N"
                        />
                    </PaxConfiguration>
                </PaxConfigurations>
            </Itinerary>
        </Itineraries>
        <Supplements>
            <PaymentMethods>
                <PaymentMethod paymentType="CreditCard" cardType="AX">
                    <PaymentCharge currency="EUR" fixAmount="9.00" minFixAmount="0"
                        appliesFixAmount="BySegment" percentage="0" minAmountPercentage="0"
                        percentageApplied="BySegment"/>
                </PaymentMethod>
                <PaymentMethod paymentType="CreditCard" cardType="VI">
                    <PaymentCharge currency="EUR" fixAmount="9.00" minFixAmount="0"
                        appliesFixAmount="BySegment" percentage="0" minAmountPercentage="0"
                        percentageApplied="BySegment"/>
                </PaymentMethod>
            </paymentMethod>
            <BaggageType>
                <BaggageType checkInType="OnLine" appliesSegments="Ida">
                    <Baggage type="bag" quantity="1" maxWeightPerUnit="0" maxTotalWeight="0"
                        paymentInAirpot="false" needToken="false">
                        <BaggageCharge currency="EUR" fixAmount="0" minFixAmount="0"
                            appliesFixAmount="ByPassenger" percentage="0" minAmountPercentage="0"
                            percentageApplied="BySegment"/>
                    </Baggage>
                </BaggageType>
                <BaggageType checkInType="OnLine" appliesSegments="Vuelta">
                    <Baggage type="bag" quantity="1" maxWeightPerUnit="0" maxTotalWeight="0"
                        paymentInAirpot="false" needToken="false">
                        <BaggageCharge currency="EUR" fixAmount="0" minFixAmount="0"
                            appliesFixAmount="ByPassenger" percentage="0" minAmountPercentage="0"
                            percentageApplied="BySegment"/>
                    </Baggage>
                </BaggageType>
                <BaggageType checkInType="OnLine" appliesSegments="Ref">
                    <References>
                        <SegmentReferences>
                            <SegmentReference itineraryRef="1" journeyRef="0" segmentRef="0"/>
                            <SegmentReference itineraryRef="1" journeyRef="0" segmentRef="1"/>
                        </SegmentReferences>
                        <PaxReferences>
                            <PaxReference paxRef="0"/>
                        </PaxReferences>
                    </References>
                    <Baggage id="D#0GO" type="bag" quantity="1" maxWeightPerUnit="0"
                        maxTotalWeight="0" paymentInAirpot="false" code="XBAG" needToken="true"
                        token="[\sA-Z0-9]{1,50}" description="23 KG BAGGAGE">
                        <BaggageCharge currency="EUR" fixAmount="50.00" minFixAmount="0"
                            appliesFixAmount="ByPassenger" percentage="0" minAmountPercentage="0"
                            percentageApplied="BySegment"/>
                    </Baggage>
                </BaggageType>
            </BaggageType>
            <Seating>
                <BlockRules>
                    <BlockRule>
                        <References>
                            <BlockReferences>
                                <BlockReference blockTypeRef="CABIN" blockRef="0"/>
                            </BlockReferences>
                            <PaxReferences>
                                <PaxReference paxRef="0"/>
                                <PaxReference paxRef="1"/>
                                <PaxReference paxRef="2"/>
                                <PaxReference paxRef="3"/>
                            </PaxReferences>
                        </References>
                        <BlockPrice>
                            <Amount currency="EUR" amount="0" amountType="FEE"/>
                        </BlockPrice>
                    </BlockRule>
                    <BlockRule>
                        <References>
                            <BlockReferences>
                                <BlockReference blockTypeRef="CABIN" blockRef="1"/>
                            </BlockReferences>
                            <PaxReferences>
                                <PaxReference paxRef="0"/>
                                <PaxReference paxRef="1"/>
                                <PaxReference paxRef="2"/>
                                <PaxReference paxRef="3"/>
                            </PaxReferences>
                        </References>
                        <BlockPrice>
                            <Amount currency="EUR" amount="0" amountType="FEE"/>
                        </BlockPrice>
                    </BlockRule>
                </BlockRules>
                <Blocks>
                    <Block type="CABIN" id="0">
                        <References>
                            <SegmentReferences>
                                <SegmentReferences itineraryRef="0" journeyRef="0"
                                    segmentRef="0"/>
                            </SegmentReferences>
                        </References>
                        <Blocks>
                            <Block type="ROW" number="1" id="0">
                                <Blocks>
                                    <Block type="SEAT" number="1A" id="0" token="1A">
                                        <Availability isAvailable="true"/>
                                        <BlockAttributes>
                                            <BlockAttribute type="WINDOW"/>
                                        </BlockAttributes>
                                    </Block>
                                    <Block type="SEAT" number="1B" id="1" token="1B">
                                        <Availability isAvailable="true"/>
                                        <BlockAttributes>
                                            <BlockAttribute type="MIDDLE"/>
                                        </BlockAttributes>
                                    </Block>
                                </Blocks>
                            </Block>
                            <Block type="ROW" number="2" id="1">
                                <Blocks>
                                    <Block type="SEAT" number="2A" id="0" token="2A">
                                        <Availability isAvailable="true"/>
                                        <BlockAttributes>
                                            <BlockAttribute type="WINDOW"/>
                                        </BlockAttributes>
                                    </Block>
                                    <Block type="SEAT" number="2B" id="1" token="2B">
                                        <Availability isAvailable="true"/>
                                        <BlockAttributes>
                                            <BlockAttribute type="MIDDLE"/>
                                        </BlockAttributes>
                                    </Block>
                                </Blocks>
                            </Block>
                        </Blocks>
                    </Block>
                </Blocks>
            </Seating>
            <specialSupplments>
                <SpecialSupplement id="A#0B5" type="Seat" quantity="1" code="SEAT" needToken="false"
                    description="PRE RESERVED SEAT ASSIGNMENT">
                    <References>
                        <SegmentReferences>
                            <SegmentReferences itineraryRef="0" journeyRef="0" segmentRef="0"/>
                            <SegmentReferences itineraryRef="0" journeyRef="0" segmentRef="1"
                            />
                        </SegmentReferences>
                        <PaxReferences>
                            <PaxReference paxRef="0"/>
                        </PaxReferences>
                    </References>
                    <CargoSuplemento currency="EUR" fixAmount="26.00" minFixAmount="0"
                        appliesFixAmount="ByPassenger" percentage="0" minAmountPercentage="0"
                        percentageApplied="BySegment"/>
                </SpecialSupplement>
            </specialSupplments>
            <Conditions>
                <Condition id="AMS-AGP-ONLOWM3-1-(5)">
                    <Paragraph title="AP.ADVANCE RES/TKT">
                        <!-- 0..n Sentences of the fare rule -->
                        <Sentence> </Sentence>
                        <Sentence> RESERVATIONS ARE REQUIRED FOR ALL SECTORS.</Sentence>
                        <Sentence> WAITLIST NOT PERMITTED.</Sentence>
                        <Sentence> TICKETING MUST BE COMPLETED WITHIN 1 DAY AFTER</Sentence>
                        <Sentence> RESERVATIONS ARE MADE OR AT LEAST 2 DAYS BEFORE DEPARTURE</Sentence>
                        <Sentence> WHICHEVER IS EARLIER.</Sentence>
                        <Sentence> OR - RESERVATIONS FOR ALL SECTORS AND TICKETING MUST BE</Sentence>
                        <Sentence> COMPLETED AT THE SAME TIME.</Sentence>
                        <Sentence> WAITLIST NOT PERMITTED.</Sentence>
                        <Sentence> NOTE -</Sentence>
                        <Sentence> WARNING-</Sentence>
                        <Sentence> ALL RESERVATIONS MADE WITHOUT TICKET NUMBER WILL</Sentence>
                        <Sentence> BE CANCELLED AUTOMATICALLY AFTER TICKETING</Sentence>
                        <Sentence> DEADLINE.</Sentence>
                    </Paragraph>
                </Condition>
                <Condition id="AGP-AMS-SHTOWMP1-1-(5)">
                    <Paragraph title="AP.ADVANCE RES/TKT">
                        <Sentence> </Sentence>
                        <Sentence> RESERVATIONS ARE REQUIRED FOR ALL SECTORS.</Sentence>
                        <Sentence> WHEN RESERVATIONS ARE MADE AT LEAST 7 DAYS BEFORE</Sentence>
                        <Sentence> DEPARTURE TICKETING MUST BE COMPLETED AT LEAST 7 DAYS</Sentence>
                        <Sentence> BEFORE DEPARTURE.</Sentence>
                        <Sentence> NOTE -</Sentence>
                        <Sentence> DIFFERENCE COULD EXIST BETWEEN THE CRS</Sentence>
                        <Sentence> LAST TICKETING DATE AND TTL ROBOT REMARK.</Sentence>
                        <Sentence> THE MOST RESTRICTIVE DATE PREVAILS.</Sentence>
                        <Sentence> OR - RESERVATIONS ARE REQUIRED FOR ALL SECTORS.</Sentence>
                        <Sentence> TICKETING MUST BE COMPLETED WITHIN 24 HOURS AFTER</Sentence>
                        <Sentence> RESERVATIONS ARE MADE.</Sentence>
                        <Sentence> NOTE -</Sentence>
                        <Sentence> DIFFERENCE COULD EXIST BETWEEN THE CRS</Sentence>
                        <Sentence> LAST TICKETING DATE AND TTL ROBOT REMARK.</Sentence>
                        <Sentence> THE MOST RESTRICTIVE DATE PREVAILS.</Sentence>
                        <Sentence> *** GENERAL RULE FOLLOWS ***</Sentence>
                        <Sentence> </Sentence>
                        <Sentence> NOTE -</Sentence>
                        <Sentence> DIFFERENCE COULD EXIST BETWEEN THE CRS</Sentence>
                        <Sentence> LAST TICKETING DATE AND TTL ROBOT REMARK.</Sentence>
                        <Sentence> THE MOST RESTRICTIVE DATE PREVAILS.</Sentence>
                    </Paragraph>
                </Condition>
            </Conditions>
        </Supplements>
    </ValuationRS> 

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

  <*@HasObFees>\*              1  Boo If true then there is an extra fee
                                  lea for using credit card.
                                  n   

  <*@carrier>\*                1  Str Validating carrier. Flights
                                  ing parameter.

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

  <*@commission>\*             1  Dec Commission.
                                  ima 
                                  l   

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
  -------------------------------------------------------------------------

|

ValuationSupplements
====================

This option is only shown when requested in Preferences node. The
functionality is the same has SupplementsRQ.

|

  ------------------------------------------------------------------------
  Element                       Num Typ Description
                                ber e   
  ----------------------------- --- --- ----------------------------------
  Supplements                   1       Supplements node in ValuationRS.

  PaymentMethods                0..     Contains a list of paymentMethods.
                                1       

  PaymentMethods/PaymentMethod  1..     Contains paymentMethod details.
                                n       

  <*@paymentType>\*             1   Str Payment Type (CreditCard,
                                    ing ElectronicBanking).

  <*@cardType>\*                1   Str Card type with a provider format.
                                    ing 

  PaymentMethods/PaymentMehotd/ 1       Charge of this payment.
  PaymentCharge                         

  <*@currency>\*                1   Str Currency code of the supplement
                                    ing 

  <*@fixAmount>\*               1   Dec Fix amount
                                    ima 
                                    l   

  <*@minFixAmount>\*            1   Dec Minimum fix amount to be applied.
                                    ima 
                                    l   

  <*@appliesFixAmount>\*        1   Str Fix amount applies: ByPassenger,
                                    ing BySegment, BaseAmount, Taxes,
                                        ForAdt (by adult), ForChd (by
                                        child) and ForInf (by infant).

  <*@percentage>\*              1   Dec Percentage.
                                    ima 
                                    l   

  <*@minAmountPercentage>\*     1   Dec Minimum percentage charge.
                                    ima 
                                    l   

  <*@percentageApplied>\*       1   Str Percentage applied: ByPassenger,
                                    ing BySegment, BaseAmount, Taxes,
                                        ForAdt (by adult), ForChd (by
                                        child) and ForInf (by infant).

  BaggageTypes                  0..     List of Baggage information.
                                1       

  BaggageTypes/BaggageType      1..     Baggage information.
                                n       

  <*@checkInType>\*             1   Str Check-in type (OnLine, Airport)
                                    ing 

  <*@appliesSegments>\*         1   Str Segments in which is applied: All,
                                    ing Departure, Return, Ref.

  BaggageTypes/BaggageType/Bagg 1..     Baggage description and charge.
  age                           n       

  <*@id>\*                      1   Str Unique identifier of the Baggage.
                                    ing 

  <*@type>\*                    1   Str Type of baggage: Bag, Bike,
                                    ing Wheelchair, Skis and BabyTrolley.

  <*@quantity>\*                1   Int Baggage quantity
                                    ege 
                                    r   

  <*@maxWeightPerUnit>\*        1   Int Maximum weight of the baggage.
                                    ege 
                                    r   

  <*@maxTotalWeight>\*          1   Int Maximum weight of ALL the baggage.
                                    ege 
                                    r   

  <*@paymentInAirpot>\*         1   Boo Determines whether the pay is in
                                    lea station.
                                    n   

  <*@code>\*                    1   Str Code of the Baggage.
                                    ing 

  <*@carrier>\*                 1   Str Carrier.
                                    ing 

  <*@needToken>\*               1   Boo Reserve token mandatory.
                                    lea 
                                    n   

  BaggaesInfos/BaggageType/Bagg 1       Charge of this payment.
  age/BaggageCharge                     

  <*@currency>\*                1   Str Currency code of the supplement
                                    ing 

  <*@fixAmount>\*               1   Dec Fix amount
                                    ima 
                                    l   

  <*@minFixAmount>\*            1   Dec Minimum fix amount to be applied.
                                    ima 
                                    l   

  <*@appliesFixamount>\*        1   Str Fix amount applies: ByPassenger,
                                    ing BySegment, BaseAmount, Taxes,
                                        ForAdt (by adult), ForChd (by
                                        child) and ForInf (by infant).

  <*@percentage>\*              1   Dec Percentage.
                                    ima 
                                    l   

  <*@minamountPercentage>\*     1   Dec Minimum percentage charge
                                    ima 
                                    l   

  <*@percentageApplied>\*       1   Str Percentage applied: ByPassenger,
                                    ing BySegment, BaseAmount, Taxes,
                                        ForAdt (by adult), ForChd (by
                                        child) and ForInf (by infant).

  BaggageTypes/BaggageType/Refe 0..     Contains a list References.
  rences                        1       

  BaggageTypes/BaggageType/Refe 0..     List of SegmentInfo References.
  rences/SegmentReferences      1       

  BaggageTypes/BaggageType/Refe 0..     SegmentInfo Reference.
  rences/SegmentReferences/Segm n       
  entReference                          

  <*@itineraryRef>\*            1   Int Itinerary Reference.
                                    ege 
                                    r   

  <*@journeyRef>\*              1   Int Journey Reference.
                                    ege 
                                    r   

  <*@segmentRef>\*              1   Int SegmentInfo Reference.
                                    ege 
                                    r   

  BaggageTypes/BaggageType/Refe 0..     List of references to passengers
  rences/PaxReferences          1       related to the baggage
                                        information.

  BaggageTypes/BaggageType/Refe 0..     Contains PaxReference details.
  rences/PaxReferences/PaxRefer n       
  ence                                  

  <*@paxRef>\*                  1   Int Unique identifier of the
                                    ege PaxReference.
                                    r   

  Seating                       0..     Seating availability.
                                1       

  Seating/BlockRules            0..     Blocks of references.
                                n       

  Seating/BlockRules/BlockRule  0..     Block of references.
                                n       

  Seating/BlockRules/BlockRule/ 0..     List of references to Blocks
  References                    1       (seating details), Segments and
                                        Passengers

  Seating/BlockRules/BlockRule/ 0..     References to block elements.
  References/BlockReferences    1       

  Seating/BlockRules/BlockRule/ 0..     List of references.
  References/BlockReferences/Bl n       
  ockReference                          

  <*@blockTypeRef>\*            1   Str Referenced block type:
                                    ing UNASSIGNED(Unassigned), AIRLINE
                                        (Airline)

  <*@blockRef>\*                1   Int Reference to block id
                                    ege 
                                    r   

  Seating/BlockRules/BlockRule/ 0..     References to Passenger.
  References/PaxReferences      1       

  Seating/BlockRules/BlockRule/ 0..     Reference to a Passenger.
  References/PaxReferences/PaxR n       
  eference                              

  <*@paxRef>\*                  1   Int The id number of the passenger
                                    ege referenced.
                                    r   

  Seating/BlockRules/BlockRule/ 0..     Price element
  BlockPrice                    1       

  Seating/BlockRules/BlockRule/ 1       Amount by type.
  BlockPrice/Amount                     

  <*@currency>\*                1   Str Currency code of the amount.
                                    ing 

  <*@amount>\*                  1   Dec Amount.
                                    ima 
                                    l   

  <*@amountType>\*              1   Str Amount type: AMOUNT (Amount), FEE
                                    ing (Service Fee), TOTAL (Total),
                                        PERCENTUAL (Percentual)

  Seating/Blocks                0..     Seating details.
                                1       

  Seating/Blocks/Block          0..     Cabin block.
                                n       

  <*@type>\*                    1   Str Type (CABIN)
                                    ing 

  <*@id>\*                      1   Int Unique id.
                                    ege 
                                    r   

  Seating/Blocks/Block/Blocks/B 0..     Row block.
  lock                          n       

  <*@type>\*                    1   Str Type (ROW).
                                    ing 

  <*@id>\*                      1   Int Unique id.
                                    ege 
                                    r   

  <*@number>\*                  1   Int Row number.
                                    ege 
                                    r   

  Seating/Blocks/Block/Blocks/B 0..     Seat block.
  lock/Blocks/Block             n       

  <*@type>\*                    1   Str Type (SEAT).
                                    ing 

  <*@id>\*                      1   Int Unique id.
                                    ege 
                                    r   

  <*@number>\*                  1   Str Seat identifier.
                                    ing 

  <*@token>\*                   1   Str Reserve token.
                                    ing 

  Seating/Blocks/Block/Blocks/B 0..     Availability of the seat.
  lock/Blocks/Block/Availabilit 1       
  y                                     

  <*@isAvailable>\*             1   Str Indicates whether the seat is
                                    ing available

  Seating/Blocks/Block/Blocks/B 0..     seat attributes.
  lock/Blocks/Block/BlockAttrib 1       
  utes                                  

  Seating/Blocks/Block/Blocks/B 0..     seat attribute.
  lock/Blocks/Block/BlockAttrib n       
  utes/BlockAttribute                   

  <*@type>\*                    1   Str seat type (OVER\_WING, MIDDLE,
                                    ing AISLE, WINDOW, COMPARTMENT,
                                        LAVATORY, LUGGAGE)

  SpecialSupplements            0..     Ancillaries
                                1       

  SpecialSupplements/SpecialSup 0..     List of ancillaries
  plement                       n       

  <*@id>\*                      1   Str Identifier
                                    ing 

  <*@type>\*                    1   Str Ancillary type (Miscellaneous,
                                    ing Seat, Meal, Pet, Lounge, Baggage)

  <*@quantity>\*                1   Int Quantity
                                    ege 
                                    r   

  <*@code>\*                    1   Str Code from the provider.
                                    ing 

  <*@needToken>\*               1   Boo Reserve token mandatory.
                                    lea 
                                    n   

  <*@description>\*             1   Str Description
                                    ing 

  Conditions                    0..     List of applied fare conditions.
                                1       

  Conditions/Condition          1..     Fare condition
                                n       

  <*@id>\*                      1   Str Typified id for the fare rule.
                                    ing 

  Conditions/Condition/Paragrap 0..     Group of sentences.
  h                             n       

  <*@title>\*                   1   Str Title
                                    ing 

  Conditions/Condition/Paragrap 0.. Str Sentences of the fare rule.
  h/Sentence                    n   ing 
  ------------------------------------------------------------------------