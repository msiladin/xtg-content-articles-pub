---
title: Reservation
keywords: activities, data structure, reservation
sidebar: mydoc_sidebar
permalink: /developer-documentation/activities/DSF/reservation
---

|

ReservationRQ Example
=====================

:

    <OTA_TourActivityBookRQ
        xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
        xmlns:xsd = "http://www.w3.org/2001/XMLSchema"
        PrimaryLangID = "es">
        <ContactDetail>
            <BirthDate>1984-02-19T00:00:00</BirthDate>
            <PersonName>
                <GivenName>TestNameClient</GivenName>
                <Surname>TestApClient</Surname>
            </PersonName>
        </ContactDetail>
        <BookingInfo>
            <BasicInfo Name = "Palma Aquarium" TourActivityID = "000200515"/>
            <Schedule StartPeriod = "2014-02-26T00:00:00" EndPeriod = "2014-02-27T00:00:00"/>
            <ParticipantInfo>
                <Individual LeadCustomerInd = "true" age = "30">
                    <GivenName>TestName1</GivenName>
                    <Surname>TestAp1</Surname>
                </Individual>
            </ParticipantInfo>
            <Pricing>
                <Summary Amount = "19.660" CurrencyCode = "EUR">
                    <PricingType Extension = "PerTotal">Other_</PricingType>
                </Summary>
                <ParticipantCategory age = "30">
                    <QualifierInfo>Adult</QualifierInfo>
                    <Price
                        Amount = "19.660"
                        CurrencyCode = "EUR"/>
                </ParticipantCategory>
            </Pricing>
            <TPA_Extensions>
                <Confirmation ID = "4791780" type = "CLIENT"/>
                <!--OpenAvailability ="true" -->
                <Issue Mandatory = "true"/>
                <Attributes>
                    <!--Attributes mandatory for confirmation. Specific for IMP -->
                    <Attribute key = "idAgrupacion" value = "8181"/>
                    <Attribute key = "idPago" value = "1"/>
                </Attributes>
            </TPA_Extensions>
        </BookingInfo>
    </OTA_TourActivityBookRQ>

|

ReservationRQ Description
=========================

  --------------------------------------------------------------------------
  Element             Num Typ Description
                      ber e   
  ------------------- --- --- ----------------------------------------------
  OTA\_TourActivityBo 1       Root node.
  okRQ                        

  @PrimaryLangID      1   Str Language code (ISO 3166-1 alpha-2) format.
                          ing 

  ContactDetail       0..     Information about holder client.
                      1       

  ContactDetail/Birth 0.. Dat Holder BirthDate.
  Date                1   e   

  ContactDetail/Birth 0.. Dat Information about name holder.
  Date/PersonName     1   e   

  ContactDetail/Birth 0.. Str Name holder.
  Date/PersonName/Giv 1   ing 
  enName                      

  ContactDetail/Birth 0.. Str Surname holder.
  Date/PersonName/Sur 1   ing 
  name                        

  BookingInfo         0..     Information about specific ticket.
                      1       

  BookingInfo/BasicIn 0..     If need search by activity provider code.
  fo                  1       

  @Name               0.. Str Name of ticket.
                      1   ing 

  @TourActivityID     1   Str Code of ticket, mandatory if need search by
                          ing activity provider code.

  BookingInfo/Schedul 1       Information about dates range on which you can
  e                           enjoy the activity.

  BookingInfo/Schedul 1       Information about dates range on which you can
  e                           enjoy the activity.

  @StartPeriod        1   Dat Start date that you apply availability.
                          e   

  @EndPeriod          1   Dat End date that you apply availability.
                          e   

  BookingInfo/Categor 0..     Category of Ticket.
  yAndType            1       

  BookingInfo/Categor 0..     Category of Ticket.
  yAndType/Category   1       

  @Code               0.. Str A category code from a predefined list, if
                      1   ing Extension = "Other" then will be provider
                              code.

  @Extension          0.. Str Enter a category here if you have selected
                      1   ing "Other" from the pre-defined list.

  BookingInfo/Partici 1..     Information about all participants.
  pantInfo            n       

  @OtherInfo          0.. Str Other instructions pertaining to the pickup/
                      1   ing dropoff.

  BookingInfo/Partici 1       Information about each participant.
  pantInfo/Individual         

  @LeadCustomerInd    1   Boo When 'true', indicates that this is the 'lead'
                          lea participantr (i.e., the primary contact making
                          n   the booking).

  @Age                1   Int Age of participant.
                          ege 
                          r   

  BookingInfo/Partici 1   Str Participant Name.
  pantInfo/Individual     ing 
  /GivenName                  

  BookingInfo/Partici 1   Str Participant Surname.
  pantInfo/Individual     ing 
  /Surname                    

  Pricing/Participant 0.. Str Specifies participant type (Adult, Children or
  Category/QualifierI 1   ing Babie). If value = "Other\_" then then is
  nfo                         mandatory specify Extension provider type.

  Pricing/Participant 1       Specific price for each participantCategory.
  Category/Price              

  @Amount             1   Str ParticipantCategory price.
                          ing 

  @CurrencyCode       0.. Str Currency code (ISO 4217).
                      1   ing 

  Pricing/Participant 0..     Necessary information that we need send
  Category/TPA\_Exten 1       between calls.
  sions                       

  Pricing/Participant 0.. Str Inform about the participant types to valuate
  Category/TPA\_Exten 1   ing (if more than one type, the participant Types
  sions/DynamicToken          must be separated by ";").

  Pricing/Participant 0..     Contains information about ticket printing.
  Category/TPA\_Exten 1       
  sions/Issue                 

  @Mandatory          0.. Boo Specifies if the ticket should be printed by
                      1   lea the client.
                          n   

  Pricing/Participant 0..     Attributes that we need send between calls.
  Category/TPA\_Exten 1       
  sions/Attributes            

  Pricing/Participant 0..     Attributes that we need send between calls.
  Category/TPA\_Exten n       
  sions/Attributes/At         
  tribute                     

  @idAgrupacion       1   Str In this case, is specific attribute mandatory
                          ing for IMP. This can obtain in iFRAME, from
                              UrlSitting that we return in availabilityRS,
                              this is for preBook reservation.

  @idPago             1   Str In this case, is specific attribute mandatory
                          ing for IMP. This can obtain in iFRAME, from
                              UrlSitting that we return in availabilityRS,
                              this is for preBook reservation.
  --------------------------------------------------------------------------

|

ReservationRS Example
=====================

:

    <OTA_TourActivityBookRS>
        <ReservationDetails>
            <BasicInfo Name = "Palma Aquarium" TourActivityID = "000200515"/>
            <Confirmation ID = "1314215#1" type = "PROVIDER"/>
            <Schedule>
                <Detail>
                    <OperationTimes>
                        <OperationTime Start = "2014-03-07T21:00:00" End = "2014-03-07T23:00:00"/>
                    </OperationTimes>
                </Detail>
            </Schedule>
            <PaymentInfo Description = "El importe total de esta factura PRO-FORMA debe obrar en poder de Beds On Line, Banco: CITIBANK(Avenida de Europa, 19 - P.E. la Moraleja, 108 - Alcobendas, Madrid) Cuenta:ES35 1474 0000 10 0012272006,  SWIFT:CITIESMX,  7 das antes de la llegada de los clientes (excepto reservas de grupos. Das de antelacin fijados en el momento de la confirmacin). En la orden de pago rogamos indiquen nuestro nmero de referencia.    Gracias por su colaboracin., AVISO: CAMBIO CDIGO SWIFT"/>
            <Pricing>
                <Summary Amount = "19.660" CurrencyCode = "EUR"/>
                <ParticipantCategory age = "30">
                    <QualifierInfo>Adult</QualifierInfo>
                    <Price
                        Amount = "19.660"
                        CurrencyCode = "EUR"/>
                </ParticipantCategory>
            </Pricing>
            <TPA_Extensions>
                <Issue Mandatory = "true">
                    <Tickets>
                        <Ticket idTicket = "15782" url = "http://93.90.21.40:8080/Janto_4TICK/GetHomeTicket?xmlDoc=%0d%0a%3cGetHomeTicket++%3e%0d%0a++%3cIdCookie%3e9999999787%3c%2fIdCookie%3e%0d%0a++%3cUsuario+%2f%3e%0d%0a++%3cRefOperacion%3e15782%3c%2fRefOperacion%3e%0d%0a++%3cReimpresion%3eS%3c%2fReimpresion%3e%0d%0a%3c%2fGetHomeTicket%3e"/>
                    </Tickets>
                </Issue>
            </TPA_Extensions>
        </ReservationDetails>
    </OTA_TourActivityBookRS>

|

Reservation RS Description
==========================

  ------------------------------------------------------------------------
  Element               Num Typ Description
                        ber e   
  --------------------- --- --- ------------------------------------------
  OTA\_TourActivityBook 1       Root node.
  RS                            

  ReservationDetails    0..     Information about specific ticket.
                        1       

  ReservationDetails/Ba 0..     If need search by activity provider code.
  sicInfo               1       

  @Name                 0.. Str Name of ticket.
                        1   ing 

  @TourActivityID       0.. Str Code of ticket.
                        1   ing 

  ReservationDetails/Co 1       Contains information of the activity
  nfirmation                    booked.

  @ID                   1   Str Activity booked identifier.
                            ing 

  @type                 1   Str Activity booked type (Possible values:
                            ing "PROVIDER").

  ReservationDetails/Sc 0..     Information about dates range on which you
  hedule                1       can enjoy the activity. The same
                                information that send in request.

  ReservationDetails/Sc 0..     Information about specify dates on which
  hedule/Detail         1       you can enjoy the activity.

  ReservationDetails/Sc 0..     Information about specify dates on which
  hedule/Detail/Operati 1       you can enjoy the activity.
  onTimes                       

  ReservationDetails/Sc 0..     Information when activity starts.
  hedule/Detail/Operati 1       
  onTimes/OperationTime         

  @Start                0.. Dat Start date activity.
                        1   e   

  @End                  0.. Dat End date activity.
                        1   e   

  ReservationDetails/Pa 0..     Payment details that may be associated
  ymentInfo             1       with an individual participant, a
                                participant category and/or a group.

  @Description          0.. Str A description of the charge.
                        1   ing 

  Pricing/Summary       0..     Summary price for option, this element we
                        1       return if OpenAvailability = false

  @Amount               0.. Dec Option price.
                        1   ima 
                            l   

  @CurrencyCode         0.. Str Currency code (ISO 4217).
                        1   ing 

  Pricing/Summary/Prici 0.. Str Specifies type of the option price, if
  ngType                1   ing value = Other then is mandatory specify
                                Extension type.

  @Extension            0.. Str Specifies type of the option price.
                        1   ing 

  Pricing/ParticipantCa 0.. Str Specifies price and participant category.
  tegory                n   ing 

  @age                  0.. Int Age of participant category.
                        1   ege 
                            r   

  Pricing/ParticipantCa 0.. Str Specifies participant type (Adult,
  tegory/QualifierInfo  1   ing Children or Babie). If value = Other then
                                then is mandatory specify Extension
                                provider type.

  @Extension            0.. Str Specifies provider code of participant
                        1   ing category.

  Pricing/ParticipantCa 1       Specific price for each
  tegory/Price                  participantCategory.

  @Amount               1   Str ParticipantCategory price.
                            ing 

  @CurrencyCode         0.. Str Currency code (ISO 4217).
                        1   ing 

  TPA\_Extensions/Issue 0..     Contains information about ticket
                        1       printing.

  @Mandatory            0.. Boo Specifies if the ticket should be printed
                        1   lea by the client.
                            n   

  TPA\_Extensions/Issue 0..     Contains information about the tickets.
  /Tickets              1       

  TPA\_Extensions/Issue 1..     List of tickets.
  /Tickets/Ticket       n       

  @idTicket             1   Str Ticket identifier. This ticket can be a
                            ing one person ticket or an operation (Set of
                                one person tickets for a same activity).

  @url                  1   Str Url containing the ticket bonus.
                            ing 

  TPA\_Extensions/Attri 0..     Attributes that we need send between
  butes                 1       calls.

  TPA\_Extensions/Attri 0..     Attributes that we need send between
  butes/Attribute       n       calls.
  ------------------------------------------------------------------------

|