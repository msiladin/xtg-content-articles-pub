---
title: Reservation
keywords: transportation, data structure, flights, reservation
sidebar: mydoc_sidebar
permalink: /developer-documentation/transportation/DSF/flights/reservation
---

|

Method Goals
============

This method aims to book one or more Itineraries.

|

Request Format
==============

The request format works the same way as the Valuation request. It can
work with one or with two Itineraries. The request will also contain a
list of Passengers and the PaymentInfo, such as payment method.

|

Response Format
===============

The result returns a list of Locators (booking codes). It can be the
supplier's or the one sent in the request. It also returns all the
charges associated to the booking.

|

Remarks
=======

This method **must** be called **after** the Valuation method.

The maximum time that our systems permits before closing the connexion
is of **25000** milliseconds.

The booking data should meet the following requirements. ADVICE: All
requirements are only indicative and could change in the future.

Passenger Type: Adult: \>11 years Child: 2-11 years Infant: 0-1 years

Companies with mandatory nationality (2 digit codes): AK D7 FD I5 PQ QZ
XJ XT Z2 E9 SL

Mandatory personal identification: - (NIF, NIE) Bookings with spanish
resident discount or some of this companies: NT H2 1T ZY 9C - (Passport)
Intercontinental flights or when origin or destination are one of this
countries: CN DM JP CU US CA GM MX RU ID DO or when the airline is one
of this: RI TR SU TT 3O AT H2 NT OB U6 UN UT V0 XY E9 - Passport data
includes passport number and expedition date and expiration date. If the
company is E9 country and city of expedition must be included.

Discounts: - Spanish resident discount: first and second surname must be
included in proper mean and also resident code and zip code. - Large
Family discount: large family number must be included and also large
family code and region code.

|

ReservationRQ Example -----------------

:

    <ReservationRQ>
        <Configuration/>
        <ClientConfiguration currencyCode = "GBP"/>
        <Itineraries>
            <Itinerary id = "0" carrier = "UX">
                <Conditions/>
                <Journeys>
                    <Journey id = "0">
                        <Segments>
                            <SegmentInfo id = "0">
                                <SegmentInfo transportationId = "ZB 226" operatingCarrier = "ZB" marketingCarrier = "ZB" departureTerminal = "LGW" arrivalTerminal = "PMI" departureDate = "2014-04-08T08:00:00" arrivalDate = "2014-04-08T11:20:00" segmentStatus = "HK">
                                    <OriginLoc type = "A" code = "LGW" cityCode = "false"/>
                                    <DestinationLoc type = "A" code = "PMI" cityCode = "false"/>
                                </SegmentInfo>
                                <SegmentClasses>
                                    <SegmentClass cabinClass = "Y" class = "E" paxRef = "0" fareBasis = "EO" fareType = "PUB"/>
                                </SegmentClasses>
                                <ReservationTokens>
                                    <Attribute key = "JourneySellKey" value = "ZB~ 226~ ~~LGW~04/08/2014 08:00~PMI~04/08/2014 11:20~"/>
                                    <Attribute key = "FareSellKey" value = "0~E~~EO~ZB03~~7~X"/>
                                </ReservationTokens>
                            </SegmentInfo>
                        </Segments>
                    </Journey>
                </Journeys>
                <ChargeBreakdown currency = "GBP" totalAmount = "40.99000000">
                    <ChargeBreakdowns/>
                    <PaxBreakdowns>
                        <PaxBreakdown paxType = "ADT" amount = "40.99000000" taxes = "40.50000000" tasaDU = "0"/>
                    </PaxBreakdowns>
                </ChargeBreakdown>
                <PaxConfigurations>
                    <PaxConfiguration id = "0" paxRef = "0" age = "30" paxType = "ADT"/>
                </PaxConfigurations>
            </Itinerary>
        </Itineraries>
        <Passengers>
            <Passenger
                passengerType = "MR"
                name = "TestNom"
                surname = "TestApe"
                birthDate = "1984-03-17T00:00:00+01:00"
                codeDCO = "0"
                documentType = "NATIONAL_ID"
                documentId = "44183932N"
                documentExpiration = "2014-03-17T17:24:46.1611924+01:00"
                nationality = "ESP">
            </Passenger>
        </Passengers>
        <Client passengerType = "MR" name = "TestNom" surname = "TestApe" eMail = "transportation@xmltravelgate.com" countryPrefix = "+34" telephone = "+34 858 275 617" mobilephone = "+34 858 275 617">
            <Address zipCode = "12159" countryCode = "es">
                <Street>C/ test, 28</Street>
                <City>test</City>
            </Address>
        </Client>
        <PaymentInfo paymentInfo = "CARD">
            <PaymentDatas>
                <PaymentData paymentType = "CARD">
                    <CardInfo provType = "VI" holder = "testnom1 testape1 testape2" number = "4444333322221111" cvv = "737" expirationMonth = "06" expirationYear = "2016"/>
                </PaymentData>
            </PaymentDatas>
        </PaymentInfo>
        <Locators>
            <Locator>
                <id>Logi123456</id>
            </Locator>
        </Locators>
    </ReservationRQ>

|

ReservationRQ Description ---------------------

+--------------------------------+----+----+-------------------------------------+
| Element                        | Nu | Ty | Description                         |
|                                | mb | pe |                                     |
|                                | er |    |                                     |
+================================+====+====+=====================================+
| ReservationRQ                  | 1  |    | Root node.                          |
+--------------------------------+----+----+-------------------------------------+
| Itineraries                    | 1  |    | List of Itineraries.                |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary          | 1. |    | Details of the Itinerary.           |
|                                | .n |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@id>\*                       | 1  | In | Unique identifier of the Itinerary. |
|                                |    | te |                                     |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@fareRef>\*                  | 1  | In | Reference identifier to the         |
|                                |    | te | original Fare. Flights parameter.   |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@HasObFees>\*                | 1  | Bo | If true then there is an extra fee  |
|                                |    | ol | for using credit card.              |
|                                |    | ea |                                     |
|                                |    | n  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@carrier>\*                  | 1  | St | Validating carrier. Flights         |
|                                |    | ri | parameter.                          |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 0. |    | Contains a list of Journeys.        |
|                                | .1 |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 0. |    | Contains details of the Journeys.   |
| /Journey                       | .n |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@id>\*                       | 1  | In | Unique identifier of the Journey in |
|                                |    | te | scope.                              |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@duration>\*                 | 1  | In | Duration of the Journey in minutes. |
|                                |    | te |                                     |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 0. |    | Contains a list of Segments         |
| /Journey/Segments              | .1 |    | associated to the Journey.          |
+--------------------------------+----+----+-------------------------------------+
| > Itineraries/Itinerary/Journe | 0. |    | Contains details of the             |
| ys/Journey/Segments/Segment    | .n |    | SegmentInfo.                        |
+--------------------------------+----+----+-------------------------------------+
| <*@id>\*                       | 1  | In | Unique SegmentInfo identifier.      |
|                                |    | te |                                     |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 0. |    | Contains information of the         |
| /Journey/Segments/Segment/Segm | .n |    | SegmentInfo.                        |
| entInfo                        |    |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@id>\*                       | 1  | In | Unique identifier of the            |
|                                |    | te | SegmentInfo.                        |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@transportationId>\*         | 1  | St | Unique Id of the transportation.    |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@transportationType>\*       | 1  | St | Transport type: F ( Flight ), T (   |
|                                |    | ri | Train ), B ( Bus ) & F ( Ferry ).   |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@operatinCarrier>\*          | 1  | St | Company which operates the          |
|                                |    | ri | transportation.                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@marketingCarrier>\*         | 1  | St | Company which commercializes the    |
|                                |    | ri | transportation.                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@departureTerminal>\*        | 1  | St | Departure terminal.                 |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@arrivalTerminal>\*          | 1  | St | Arrival terminal.                   |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@departureDate>\*            | 1  | Da | Departure date.                     |
|                                |    | te |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@arrivalDate>\*              | 1  | Da | Arrival date.                       |
|                                |    | te |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@segmentDuration>\*          | 1  | In | Transport duration ( in minutes ).  |
|                                |    | te |                                     |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@planeType>\*                | 1  | St | Plane type. Flights parameter.      |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@maxCheckinDate>\*           | 1  | St | Maximum date to make the check-in.  |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@segmentStatus>\*            | 1  | St | SegmentInfo status: HK (OK), TK     |
|                                |    | ri | (Change of programming), UC         |
|                                |    | ng | (Unconfirmed), UN( Unable), NO (No  |
|                                |    |    | action taken) & UD (Undefined)      |
+--------------------------------+----+----+-------------------------------------+
| <*@hasTechnicalStop>\*         | 1  | Bo | If true, the SegmentInfo has a      |
|                                |    | ol | technical stop.                     |
|                                |    | ea |                                     |
|                                |    | n  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@electronicTicket>\*         | 1  | Bo | If true, the SegmentInfo uses a     |
|                                |    | ol | electronic ticket.                  |
|                                |    | ea |                                     |
|                                |    | n  |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 1  |    | Origin location.                    |
| /Journey/Segments/Segment/Segm |    |    |                                     |
| entInfo/OriginLoc              |    |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@type>\*                     | 1  | St | Type of station of the location     |
|                                |    | ri | indicated with A ( AirPort ), T (   |
|                                |    | ng | Train Station ) & P ( Port ).       |
+--------------------------------+----+----+-------------------------------------+
| <*@code>\*                     | 1  | St | Location code.                      |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@cityCode>\*                 | 1  | Bo | If true, the field code indicates a |
|                                |    | ol | city code, if false, it will        |
|                                |    | ea | indicate an airport code.           |
|                                |    | n  |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 1  |    | Destination location.               |
| /Journey/Segments/Segment/Segm |    |    |                                     |
| entInfo/DestinationLoc         |    |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@type>\*                     | 1  | St | Type of station of the location     |
|                                |    | ri | indicated with A ( AirPort ), T (   |
|                                |    | ng | Train Station ) & P ( Port ).       |
+--------------------------------+----+----+-------------------------------------+
| <*@code>\*                     | 1  | St | Location code.                      |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@cityCode>\*                 | 1  | Bo | If true, the field code indicates a |
|                                |    | ol | city code, if false, it will        |
|                                |    | ea | indicate an airport code.           |
|                                |    | n  |                                     |
+--------------------------------+----+----+-------------------------------------+
| Transportation/Segments/Segmen | 0. |    | Contains a list of TechnicalStops.  |
| t/TechnicalStops               | .1 |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@totalTechnicalStops>\*      | 1  | In | Total number of TechnicalStops.     |
|                                |    | te |                                     |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| Transportation/Segments/Segmen | 1. |    | Contains the details of the         |
| t/TechnicalStops/TechnicalStop | .n |    | TechnicalStop.                      |
+--------------------------------+----+----+-------------------------------------+
| <*@location>\*                 | 1  | St | TechnicalStop location.             |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@stopDate>\*                 | 1  | Da | Approx. stop date and time.         |
|                                |    | te |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@departureDate>\*            | 1  | Da | Approx. departure date and time.    |
|                                |    | te |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 0. |    | Contains a list of SegmentClasses.  |
| /Journey/Segments/Segment/Segm | .1 |    |                                     |
| entClasses                     |    |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 0. |    | Contains details of the             |
| /Journey/Segments/Segment/Segm | .n |    | SegmentClass.                       |
| entClasses/SegmentClass        |    |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@cabinClass>\*               | 1  | St | Cabin class of the seat: N (Not     |
|                                |    | ri | specified), Y (Tourist), C          |
|                                |    | ng | (Business), F (First), CA (Cabin,   |
|                                |    |    | only for ferries), YP (Tourist      |
|                                |    |    | Plus)                               |
+--------------------------------+----+----+-------------------------------------+
| <*@class>\*                    | 1  | St | Fare class.                         |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@paxRef>\*                   | 1  | In | Reference for the Passenger which   |
|                                |    | te | is using this fare in the           |
|                                |    | ge | transport.                          |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@fareBasis>\*                | 1  | St | Fare basis.                         |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@fareType>\*                 | 1  | St | Fare type: PUB ( Public ), PRI (    |
|                                |    | ri | Private ), NEGO ( Negotiated ) &    |
|                                |    | ng | CORP ( Corporate ).                 |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 0. |    | Contains specific attributes of     |
| /Journey/Segments/Segment/Rese | .1 |    | each provider.                      |
| rvationToken                   |    |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/Journeys | 0. |    | Contains details of the attribute.  |
| /Journey/Segments/Segment/Rese | .n |    |                                     |
| rvationToken/Attribute         |    |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@id>\*                       | 1  |    | Keyword or id to identify a         |
|                                |    |    | parameter.                          |
+--------------------------------+----+----+-------------------------------------+
| <*@value>\*                    | 1  |    | Value of the parameter.             |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/AmountBr | 1  |    | Contains details of the             |
| eakdown                        |    |    | AmountBreakdown.                    |
+--------------------------------+----+----+-------------------------------------+
| <*@currency>\*                 | 1  | St | Currency code of the fare.          |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@totalAmount>\*              | 1  | De | Total amount. with taxes and other  |
|                                |    | ci | charges included.                   |
|                                |    | ma |                                     |
|                                |    | l  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@notCommissionableAmount>\*  | 1  | De | Total amount that can not be        |
|                                |    | ci | commissioned.                       |
|                                |    | ma |                                     |
|                                |    | l  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@commission>\*               | 1  | De | Commission.                         |
|                                |    | ci |                                     |
|                                |    | ma |                                     |
|                                |    | l  |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/AmountBr | 0. |    | Contains a list of                  |
| eakdown/ChargeBreakdowns       | .1 |    | ChargeBreakdowns.                   |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/AmountBr | 0. |    | Contains a list of breakdown        |
| eakdown/PaxBreakdowns          | .1 |    | amounts for each Passenger ( ADT    |
|                                |    |    | amount, etc. ).                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/AmountBr | 0. |    | Contains details of breakdown       |
| eakdown/PaxBreakdowns/PaxBreak | .n |    | amounts for each Passenger.         |
| down                           |    |    |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@paxType>\*                  | 1  | St | Passenger type: ADT ( Adult ), CHD  |
|                                |    | ri | ( Child ) & INF ( Infant ).         |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@amount>\*                   | 1  | De | Total amount, with taxes included,  |
|                                |    | ci | associated to the Passenger.        |
|                                |    | ma |                                     |
|                                |    | l  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@taxes>\*                    | 1  | In | If they exist, taxes are applied    |
|                                |    | te | for this Passenger type.            |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@tasaDU>\*                   | 1  | In | Deprecated                          |
|                                |    | te |                                     |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/PaxConfi | 1  |    | Contains a list of                  |
| gurations                      |    |    | PaxConfigurations.                  |
+--------------------------------+----+----+-------------------------------------+
| Itineraries/Itinerary/PaxConfi | 1  |    | Contains details of the             |
| gurations/PaxConfiguration     |    |    | PaxConfiguration.                   |
+--------------------------------+----+----+-------------------------------------+
| <*@id>\*                       | 1  | In | Unique identifier of the            |
|                                |    | te | PaxConfiguration.                   |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@paxRef>\*                   | 1  | In | Reference to the Passenger Id from  |
|                                |    | te | the request.                        |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@age>\*                      | 1  | In | Age of the Passenger.               |
|                                |    | te |                                     |
|                                |    | ge |                                     |
|                                |    | r  |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@paxType>\*                  | 1  | St | Passenger type based on the age of  |
|                                |    | ri | the Passenger: ADT (Adult), CHD     |
|                                |    | ng | (Child), INF (Infant), YOU (Young)  |
|                                |    |    | and SEN (Senior).                   |
+--------------------------------+----+----+-------------------------------------+
| <*@code>\*                     | 1  | St | String with the PTC code.           |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Passengers                     | 1  |    | Contains a list of Passengers.      |
+--------------------------------+----+----+-------------------------------------+
| Passengers/Passenger           | 1. |    | Contains information of the         |
|                                | .n |    | Passenger.                          |
+--------------------------------+----+----+-------------------------------------+
| <*@passengerType>\*            | 1  | St | Treatment: MR, MRS, CHD and INF.    |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@name>\*                     | 1  | St | Name of the Passenger.              |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@surname>\*                  | 1  | St | Surname/s of the Passenger.         |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@bithDate>\*                 | 1  | St | Date of birth.                      |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@codeDCO>\*                  | 1  | St | Document code.                      |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@documentType>\*             | 1  | St | NATIONAL\_ID, PASSPORT,             |
|                                |    | ri | RESIDENT\_ID.                       |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@documentId>\*               | 1  | St | Unique identifier of the            |
|                                |    | ri | documentation.                      |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@documentExpiration>\*       | 1  | St | Expiration date of the              |
|                                |    | ri | documentation.                      |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@nationality>\*              | 1  | St | Nationality.                        |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Passengers/Passenger/PaxBonusD | 1  |    | Contains details of the Passenger   |
| etails                         |    |    | bonus.                              |
+--------------------------------+----+----+-------------------------------------+
| Passengers/Passenger/PaxBonusD | 1  |    | Contains details of the applied     |
| etails/AppliedBonuses          |    |    | bonus.                              |
+--------------------------------+----+----+-------------------------------------+
| <*@resident>\*                 | 1  | St | Resident.                           |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@largeFamily>\*              | 1  | St | Large family discount: N (none), F1 |
|                                |    | ri | (5% discount) and F2 (10%           |
|                                |    | ng | discount).                          |
+--------------------------------+----+----+-------------------------------------+
| <*@discountCard>\*             | 1  | St | Discount card:                      |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Client                         | 1  |    | Contains client's information.      |
+--------------------------------+----+----+-------------------------------------+
| <*@passengerType>\*            | 1  | St | Treatment.                          |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@name>\*                     | 1  | St | Name.                               |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@surname>\*                  | 1  | St | SurName.                            |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@eMail>\*                    | 1  | St | eMail address.                      |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@countryPrefix>\*            | 1  | St | Country telephone prefix.           |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@telephone>\*                | 1  | St | Telephone.                          |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@mobilephone>\*              | 1  | St | mobilephone Telephone.              |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Client/Address                 | 1  |    | Contains the client's address.      |
+--------------------------------+----+----+-------------------------------------+
| <*@zipCode>\*                  | 1  | St | Zip code.                           |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@countryCode>\*              | 1  | St | Country code.                       |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Client/Address/Street          | 1  | St | Contains the street name of the     |
|                                |    | ri | address.                            |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Client/Address/City            | 1  | St | Contains the locality.              |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| PaymentInfo                    | 1  |    | Contains the information of the     |
|                                |    |    | payment.                            |
+--------------------------------+----+----+-------------------------------------+
| <*@paymentInfo>\*              | 1  | St | Payment type.                       |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| PaymentInfo/PaymentDatas       | 1  |    | Contains a list of payment data.    |
+--------------------------------+----+----+-------------------------------------+
| PaymentInfo/PaymentDatas/Payme | 1  |    | Contains details of the payment     |
| ntData                         |    |    | data.                               |
+--------------------------------+----+----+-------------------------------------+
| <*@paymentType>\*              | 1  | St | Payment type: CASH, CARD and EMIT.  |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| PaymentInfo/PaymentDatas/Payme | 1  |    | Contains details of the credit      |
| ntData/CardInfo                |    |    | card.                               |
+--------------------------------+----+----+-------------------------------------+
| <*@provType>\*                 | 1  | St | Card type.                          |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@holder>\*                   | 1  | St | Holder.                             |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@number>\*                   | 1  | St | Credit card number.                 |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@cvv>\*                      | 1  | St | Verification code.                  |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@expirationMonth>\*          | 1  | St | Expiration month.                   |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| <*@expirationYear>\*           | 1  | St | Expiration year.                    |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Locators                       | 1  |    | Contains a list of locators.        |
+--------------------------------+----+----+-------------------------------------+
| Locators/Locator               | 1  |    | Contains details of the locator.    |
+--------------------------------+----+----+-------------------------------------+
| Locators/Locator/Id            | 1  | St | Unique identifier of the locator.   |
|                                |    | ri |                                     |
|                                |    | ng |                                     |
+--------------------------------+----+----+-------------------------------------+
| Locators/Locator/Type          | 1  | St | Locator type: PROVIDER,             |
|                                |    | ri | TFBOOKINGREFERENCE, UNIVERSAL,      |
|                                |    | ng | EMISSION and CARRIER.               |
+--------------------------------+----+----+-------------------------------------+

|

ReservationsRS Example -----------------

    <ReservationsRS>
        <Passengers>
            <Passenger
                passengerType = "MR"
                name = "TestNom"
                surname = "TestApe"
                birthDate = "1984-03-10T23:00:00"
                codeDCO = "0"
                documentType = "NATIONAL_ID"
                documentExpiration = "0001-01-01T00:00:00"
                nationality = ""
                Sexo = "72"
                resident = "NO_VERIFICADO">
            </Passenger>
        </Passengers>
        <Locators>
            <id>KENHSR</id>
            <Type>PROVEEDOR</Type>
        </Locators>
        <Locators>
            <id>225901#</id>
            <Type>TFBOOKINGREFERENCE</Type>
        </Locators>
        <Invoice>
            <AmountBreakdown currency = "GBP" totalAmount = "40.99000000">
                <ChargeBreakdowns/>
                <PaxBreakdowns>
                    <PaxBreakdown paxType = "ADT" amount = "40.99000000"/>
                </PaxBreakdowns>
            </AmountBreakdown>
        </Invoice>
    </ReservationsRS>

|

ReservationsRS Description ---------------------

  ------------------------------------------------------------------------
  Element                        Nu Ty Description
                                 mb pe 
                                 er    
  ------------------------------ -- -- -----------------------------------
  ReservationsRS                 1     Root node.

  Passengers                     1     Contains a list of Passengers.

  Passengers/Passenger           1.    Contains information of the
                                 .n    Passenger.

  <*@passengerType>\*            1  St Treatment: MR, MRS, CHD and INF.
                                    ri 
                                    ng 

  <*@name>\*                     1  St Name of the Passenger.
                                    ri 
                                    ng 

  <*@surname>\*                  1  St Surname/s of the Passenger.
                                    ri 
                                    ng 

  <*@bithDate>\*                 1  St Date of birth.
                                    ri 
                                    ng 

  <*@codeDCO>\*                  1  St Document code.
                                    ri 
                                    ng 

  <*@documentType>\*             1  St Documentation type.
                                    ri 
                                    ng 

  <*@documentId>\*               1  St Unique identifier of the
                                    ri documentation.
                                    ng 

  <*@documentExpiration>\*       1  St Expiration date of the
                                    ri documentation.
                                    ng 

  <*@nationality>\*              1  St Nationality.
                                    ri 
                                    ng 

  Locators                       1     Contains a list of locators.

  Locators/Locator               1     Contains details of the locator.

  Locators/Locator/Id            1  St Unique identifier of the locator.
                                    ri 
                                    ng 

  Locators/Locator/Type          1  St Locator type: PROVIDER,
                                    ri TFBOOKINGREFERENCE, UNIVERSAL,
                                    ng EMISSION and CARRIER.

  Invoice                        1     

  Invoice/AmountBreakdown        1     

  <*@currency>\*                 1  St Currency code of the fare.
                                    ri 
                                    ng 

  <*@totalAmount>\*              1  De Total amount. with taxes and other
                                    ci charges included.
                                    ma 
                                    l  

  <*@notCommissionableAmount>\*  1  De Total amount that can not be
                                    ci commissioned.
                                    ma 
                                    l  

  <*@commission>\*               1  De Commission.
                                    ci 
                                    ma 
                                    l  

  Invoice/AmountBreakdown/Charge 0.    Contains a list of
  Breakdowns                     .1    ChargeBreakdowns.

  Invoice/AmountBreakdown/PaxBre 0.    Contains a list of breakdown
  akdowns                        .1    amounts for each Passenger ( ADT
                                       amount, etc. ).

  Invoice/AmountBreakdown/PaxBre 0.    Contains details of breakdown
  akdowns/PaxBreakdown           .n    amounts for each Passenger.

  <*@paxType>\*                  1  St Passenger type: ADT ( Adult ), CHD
                                    ri ( Child ) & INF ( Infant ).
                                    ng 

  <*@amount>\*                   1  De Total amount, with taxes included,
                                    ci associated to the Passenger.
                                    ma 
                                    l  

  <*@taxes>\*                    1  In If they exist, taxes are applied
                                    te for this Passenger type.
                                    ge 
                                    r  

  <*@tasaDU>\*                   1  In Deprecated
                                    te 
                                    ge 
                                    r  
  ------------------------------------------------------------------------

|