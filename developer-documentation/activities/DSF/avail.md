---
title: Avail
keywords: activities, data structure, avail
sidebar: mydoc_sidebar
permalink: /developer-documentation/activities/DSF/avail
---

|

Method Goals
============

This method aims to return all the available options for a given date
and search type. It does not filter different classes, times or fares.
It will always return all results returned by the supplier between
specific date range.

|

Request Format
==============

It is mandatory to pass a date range and a search type. Depends if
OpenAvailability is true or false (this attribute return in
StaticConfiguration call), you need specify passengers.

**Search types**

-   RegionCode : Specify a provider region code where you want to
    perform availability.
-   Activity ID : Specify a provider activity code of the desired
    activity.
-   Category/Code : Specify a provider category code of the desired
    activity category.

|

Response Format
===============

The response contains information of each activity that provider return.
Depends if OpenAvailability is true or false (this attribute return in
StaticConfiguration call).

**OpenAvailability**

-   OpenAvailability = false: Need specify passangers in avail request.
    In response, provider return price of option that you specify.
-   OpenAvailability = true: Not neccesary specify passangers in avail
    request. In this case provider return all possible participant types
    that can provide, and you can choose the participants types that you
    are interested.

|

AvailRQ Example
===============

:

    <OTA_TourActivityAvailRQ
        xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
        xmlns:xsd = "http://www.w3.org/2001/XMLSchema"
        PrimaryLangID = "es">
        <TourActivity>
            <!--Search by activity provider code-->
            <BasicInfo TourActivityID = "PRUEBAPORESPECT1"/>
            <Schedule StartPeriod = "2014-03-20T00:00:00" EndPeriod = "2014-03-21T00:00:00"/>
            <!--Search by provider category code-->
            <CategoryAndTypes>
                <Category Code = "1" Extension = "Other"/>
            </CategoryAndTypes>
            <Schedule StartPeriod = "2014-03-20T00:00:00" EndPeriod = "2014-03-21T00:00:00"/>
            <!--Search by provider region code-->
            <Location>
                <Region RegionCode = "PMI"/>
            </Location>
            <!--Mandatory specify if OpenAvailability = false-->
            <ParticipantCount Age = "30" Quantity = "1"/>
        </TourActivity>
    </OTA_TourActivityAvailRQ>

|

AvailRQ Description
===================

  -------------------------------------------------------------------------
  Element              Numb Type  Description
                       er         
  -------------------- ---- ----- -----------------------------------------
  OTA\_TourActivityAva 1          Root node.
  ilRQ                            

  @PrimaryLangID       1    Strin Language code (ISO 3166-1 alpha-2)
                            g     format..

  TourActivityInfo     0..n       Information about specific ticket.

  TourActivityInfo/Bas 0..1       If need search by activity provider code.
  icInfo                          

  @Name                0..1 Strin Name of ticket.
                            g     

  @TourActivityID      0..1 Strin Code of ticket, mandatory if need search
                            g     by activity provider code.

  TourActivityInfo/Sch 1          Information about dates range on which
  edule                           you can enjoy the activity.

  TourActivityInfo/Sch 1          Information dates range that you apply
  edule/Summary                   availability.

  @Start               1    Date  Start date that you apply availability.

  @End                 1    Date  End date that you apply availability.

  TourActivityInfo/Cat 0..1       Category of Ticket.
  egoryAndType/Categor            
  y                               

  @Code                0..1 Strin A category code from a predefined list,
                            g     if Extension = "Other" then will be
                                  provider code.

  @Extension           0..1 Strin Enter a category here if you have
                            g     selected "Other" from the pre-defined
                                  list.

  TourActivityInfo/Cat 0..1       Category of Ticket.
  egoryAndType                    

  TourActivityInfo/Cat 0..1       Category of Ticket.
  egoryAndType/Categor            
  y                               

  @Code                0..1 Strin A category code from a predefined list,
                            g     if Extension = "Other" then will be
                                  provider code.

  @Extension           0..1       Enter a category here if you have
                                  selected "Other" from the pre-defined
                                  list.

  Location             0..1       The location of the tour/ activity.

  Location/Region      0..1       Describes regional information.

  @RegionCode          0..1 Strin Specifies a region code.
                            g     

  @RegionName          0..1 Strin Specifies the region name.
                            g     

  ParticipantCount     0..n       Information about participant type,
                                  specifying age for each participant.

  @Age                 1    Integ Age of participant.
                            er    

  @Quantity            1    Integ Number of participant with same age.
                            er    
  -------------------------------------------------------------------------

|

AvailRS Example
===============

:

    <OTA_TourActivityAvailRS xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd = "http://www.w3.org/2001/XMLSchema">
        <!--OpenAvailability = false -->
        <TourActivityInfo>
            <BasicInfo Name = "Palma Aquarium" TourActivityID = "000200515"/>
            <Schedule>
                <Summary Start = "2014-03-20T00:00:00" End = "2014-03-21T00:00:00"/>
                <Detail>
                    <OperationTimes>
                        <OperationTime Start = "2014-03-20T00:00:00" End = "2014-03-20T00:00:00"/>
                    </OperationTimes>
                    <!-- Attributes required to pass between calls or information necessary for the client-->
                    <TPA_Extensions>
                        <Attributes>
                            <Attribute key = "availToken" value = "BpvkqOrfqU6ZpOqiJ0k21g=="/>
                            <Attribute key = "modalityCode" value = "0#8"/>
                            <Attribute key = "dateFrom" value = "20140320"/>
                            <Attribute key = "dateTo" value = "20140320"/>
                            <Attribute key = "limitAdult" value = "12"/>
                            <Attribute key = "modeCode" value = "P"/>
                        </Attributes>
                    </TPA_Extensions>
                </Detail>
                <Detail>
                    <OperationTimes>
                        <OperationTime Start = "2014-03-21T00:00:00" End = "2014-03-21T00:00:00"/>
                    </OperationTimes>
                    <TPA_Extensions>
                        <Attributes>
                            <Attribute key = "availToken" value = "BpvkqOrfqU6ZpOqiJ0k21g=="/>
                            <Attribute key = "modalityCode" value = "0#8"/>
                            <Attribute key = "dateFrom" value = "20140321"/>
                            <Attribute key = "dateTo" value = "20140321"/>
                            <Attribute key = "limitAdult" value = "12"/>
                            <Attribute key = "modeCode" value = "P"/>
                        </Attributes>
                    </TPA_Extensions>
                </Detail>
            </Schedule>
            <Location>
                <Region RegionCode = "PMI"/>
            </Location>
            <Description>
                <ShortDescription>Descubre los secretos mejor guardados del mundo marino recorriendo los rincones de este maravilloso parque marino con ms de 8.000 animales de 700 especies diferentes y ms de 5 millones de litros de agua salada. Recorre los 900 metros que forman el itinerario del parque y descubre los espectaculares secretos que esconde en su interior. Adems podrs disfrutar de un sinfn de actividades que te permitirn combinar un amplio conocimiento del fondo del mar.</ShortDescription>
                <Multimedia>
                    <MultimediaDescription>
                        <ImageItems>
                            <ImageItem>
                                <ImageFormat>
                                    <URL>http://www.hotelbeds.com/giata/extras/big/ds/11479/11479_4.jpg</URL>
                                </ImageFormat>
                            </ImageItem>
                            <ImageItem>
                                <ImageFormat>
                                    <URL>http://www.hotelbeds.com/giata/extras/big/ds/11479/11479_1.jpg</URL>
                                </ImageFormat>
                            </ImageItem>
                            <ImageItem>
                                <ImageFormat>
                                    <URL>http://www.hotelbeds.com/giata/extras/big/ds/11479/11479_2.jpg</URL>
                                </ImageFormat>
                            </ImageItem>
                            <ImageItem>
                                <ImageFormat>
                                    <URL>http://www.hotelbeds.com/giata/extras/big/ds/11479/11479_3.jpg</URL>
                                </ImageFormat>
                            </ImageItem>
                            <ImageItem>
                                <ImageFormat>
                                    <URL>http://www.hotelbeds.com/giata/extras/big/ds/11479/11479_4.jpg</URL>
                                </ImageFormat>
                            </ImageItem>
                            <ImageItem>
                                <ImageFormat>
                                    <URL>http://www.hotelbeds.com/giata/extras/big/ds/11479/11479_5.jpg</URL>
                                </ImageFormat>
                            </ImageItem>
                            <ImageItem>
                                <ImageFormat>
                                    <URL>http://www.hotelbeds.com/giata/extras/big/ds/11479/11479_6.jpg</URL>
                                </ImageFormat>
                            </ImageItem>
                        </ImageItems>
                    </MultimediaDescription>
                </Multimedia>
            </Description>
            <Pricing>
                <Summary Amount = "19.661" CurrencyCode = "EUR">
                    <PricingType Extension = "PerPersonPerDay">Other_</PricingType>
                </Summary>
                <ParticipantCategory age = "30">
                    <QualifierInfo>Adult</QualifierInfo>
                    <Price
                        Amount = "19.661"
                        CurrencyCode = "EUR"/>
                </ParticipantCategory>
            </Pricing>
        </TourActivityInfo>
        <!--OpenAvailability = true-->
        <TourActivityInfo>
            <BasicInfo Name = "La Prueba Final (EVENTO DE PRUEBA)" TourActivityID = "PRUEBAPORESPECT1"/>
            <Schedule>
                <Summary Start = "2014-02-26T00:00:00" End = "2014-02-27T00:00:00"/>
                <Detail>
                    <OperationTimes>
                        <OperationTime Start = "2014-02-26T20:00:00"/>
                    </OperationTimes>
                </Detail>
            </Schedule>
            <CategoryAndType>
                <Category Code = "1" Extension = "Other"/>
            </CategoryAndType>
            <Location>
                <Region RegionCode = "20" RegionName = "Madrid"/>
                <Address>
                    <AddressLine>-</AddressLine>
                    <PostalCode/>
                    <County>ESPAA</County>
                </Address>
            </Location>
            <Pricing>
                <ParticipantCategory>
                    <QualifierInfo Extension = "27#pr1">Other</QualifierInfo>
                    <Price
                        Amount = "5"
                        CurrencyCode = "EUR"/>
                    <!-- Attributes required to pass between calls and information necessary for the client-->
                    <TPA_Extensions>
                        <Seat>
                            <Level id = "N1" description = "Nivel 1"/>
                            <Area id = "A1" description = "Area 1"/>
                            <Zone id = "A1_z1" description = "Parte Central"/>
                            <Sector id = "A1_z1_b1" description = "Delantera Derecha"/>
                            <UrlSitting>http://93.90.21.41/Janto/traveltino/public/janto/main.php?Nivel=Detalle_1_Sesion&Idioma=es&idSesion=0000000000000211&idZona=A1_z1&idBloque=A1_z1_b1&idConcesion=XXX&numEntradas=1&modo=IFRAME</UrlSitting>
                        </Seat>
                        <DynamicToken/>
                        <Issue Mandatory = "false"/>
                        <Attributes>
                            <Attribute key = "idSesion" value = "0000000000000211"/>
                        </Attributes>
                    </TPA_Extensions>
                </ParticipantCategory>
                <ParticipantCategory>
                    <QualifierInfo Extension = "27#pr2">Other</QualifierInfo>
                    <Price
                        Amount = "2"
                        CurrencyCode = "EUR"/>
                    <TPA_Extensions>
                        <Seat>
                            <Level id = "N1" description = "Nivel 1"/>
                            <Area id = "A1" description = "Area 1"/>
                            <Zone id = "A1_z1" description = "Parte Central"/>
                            <Sector id = "A1_z1_b1" description = "Delantera Derecha"/>
                            <UrlSitting>http://93.90.21.41/Janto/traveltino/public/janto/main.php?Nivel=Detalle_1_Sesion&Idioma=es&idSesion=0000000000000211&idZona=A1_z1&idBloque=A1_z1_b1&idConcesion=XXX&numEntradas=1&modo=IFRAME</UrlSitting>
                        </Seat>
                        <DynamicToken/>
                        <Issue Mandatory = "false"/>
                        <Attributes>
                            <Attribute key = "idSesion" value = "0000000000000211"/>
                        </Attributes>
                    </TPA_Extensions>
                </ParticipantCategory>
            </Pricing>
        </TourActivityInfo>
                    .
                    .
    </OTA_TourActivityAvailRS>

|

AvailRS Description
===================

  -------------------------------------------------------------------------
  Element                   Num Typ Description
                            ber e   
  ------------------------- --- --- ---------------------------------------
  OTA TourActivityAvailRS   1       Root node.

  TourActivityInfo          0..     Information about specific ticket.
                            n       

  TourActivityInfo/BasicInf 0..     Basic Information of ticket.
  o                         1       

  @Name                     0.. Str Name of ticket.
                            1   ing 

  @TourActivityID           0.. Str Code of ticket.
                            1   ing 

  TourActivityInfo/Schedule 1       Information about dates range on which
                                    you can enjoy the activity.

  TourActivityInfo/Schedule 1       Information dates range that you apply
  /Summary                          availability.

  @Start                    1   Dat Start date that you apply availability.
                                e   

  @End                      1   Dat End date that you apply availability.
                                e   

  TourActivityInfo/Schedule 0..     Information when activity starts and
  /Detail                   1       attributes that we need send between
                                    calls.

  TourActivityInfo/Schedule 0..     Information when activity starts.
  /Detail/OperationTimes    1       

  TourActivityInfo/Schedule 0..     Information when activity starts.
  /Detail/OperationTimes/Op 1       
  erationTime                       

  @Start                    0.. Dat Start date activity.
                            1   e   

  @End                      0.. Dat End date activity.
                            1   e   

  TourActivityInfo/Schedule 0..     Necessary information that we need send
  /Detail/TPA\_Extensions   1       between calls.

  TourActivityInfo/Schedule 0..     Attributes that we need send between
  /Detail/TPA\_Extensions/A 1       calls.
  ttributes                         

  TourActivityInfo/Schedule 0..     Attributes that we need send between
  /Detail/TPA\_Extensions/A n       calls.
  ttributes/Attribute               

  TourActivityInfo/Category 0..     Category of Ticket.
  AndType                   1       

  TourActivityInfo/Category 0..     Category of Ticket.
  AndType/Category          1       

  @Code                     0.. Str A category code from a predefined list,
                            1   ing if Extension = "Other" then will be
                                    provider code.

  @Extension                0.. Str Enter a category here if you have
                            1   ing selected "Other" from the pre-defined
                                    list.

  Location                  1       The location of the tour/ activity.

  Location/Region           1       Describes regional information.

  @RegionCode               1   Str Specifies a region code.
                                ing 

  @RegionName               1   Str Specifies the region name.
                                ing 

  Location/Address          0..     Identifies the physical address of the
                            1       tour departure and/or activity
                                    location.

  Location/Address/AddressL 0.. Str These lines will contain free form
  ine                       1   ing address details.

  Location/Address/PostalCo 0.. Str Post Office Code number.
  de                        1   ing 

  Location/Address/County   0.. Str County or Region Name.
                            1   ing 

  Description               0..     Images and descriptions of the
                            1       activity.

  Description/ShortDescript 0.. Str Short description of the activity.
  ion                       1   ing 

  Description/Multimedia    0..     Information and url images.
                            1       

  Description/Multimedia/Mu 0..     Information and url images.
  ltimediaDescription       1       

  Description/Multimedia/Mu 0..     Information and url images.
  ltimediaDescription/Image 1       
  Items                             

  Description/Multimedia/Mu 0..     Information for each image.
  ltimediaDescription/Image n       
  Items/ImageItem                   

  Description/Multimedia/Mu 0..     Url image.
  ltimediaDescription/Image 1       
  Items/ImageItem/ImageForm         
  at                                

  Description/Multimedia/Mu 0.. Str Access to image url.
  ltimediaDescription/Image 1   ing 
  Items/ImageItem/ImageForm         
  at/URL                            

  Pricing                   1       Price for option if OpenAvailability =
                                    false and price for each
                                    participantCategory if OpenAvailability
                                    = true.

  Pricing/Summary           0..     Summary price for option, this element
                            1       we return if OpenAvailability = false

  @Amount                   0.. Dec Option price.
                            1   ima 
                                l   

  @CurrencyCode             0.. Str Currency code (ISO 4217).
                            1   ing 

  Pricing/Summary/PricingTy 0.. Str Specifies type of the option price, if
  pe                        1   ing value = Other then is mandatory specify
                                    Extension type.

  @Extension                0.. Str Specifies type of the option price.
                            1   ing 

  Pricing/ParticipantCatego 0.. Str Specifies price and participant
  ry                        n   ing category.

  @age                      0.. Int Age of participant category.
                            1   ege 
                                r   

  Pricing/ParticipantCatego 0.. Str Specifies participant type (Adult,
  ry/QualifierInfo          1   ing Children or Babie). If value = Other
                                    then then is mandatory specify
                                    Extension provider type.

  @Extension                0.. Str Specifies provider code of participant
                            1   ing category.

  Pricing/ParticipantCatego 1       Specific price for each
  ry/Price                          participantCategory.

  @Amount                   1   Str ParticipantCategory price.
                                ing 

  @CurrencyCode             0.. Str Currency code (ISO 4217).
                            1   ing 

  Pricing/ParticipantCatego 0..     Necessary information that we need send
  ry/TPA\_Extensions        1       between calls.

  Pricing/ParticipantCatego 0..     Information about location of seat.
  ry/TPA\_Extensions/Seat   1       

  Pricing/ParticipantCatego 0..     Information about level/floor of seat.
  ry/TPA\_Extensions/Level  1       

  Pricing/ParticipantCatego 0..     Area where the site is located.
  ry/TPA\_Extensions/Area   1       

  Pricing/ParticipantCatego 0..     Zone where the site is located.
  ry/TPA\_Extensions/Zone   1       

  Pricing/ParticipantCatego 0..     Sector where the site is located.
  ry/TPA\_Extensions/Sector 1       

  Pricing/ParticipantCatego 0..     Specify the interface provider access
  ry/TPA\_Extensions/UrlSit 1       where client can choose seat.
  ting                              

  @id                       0.. Str Provider code about location of seat.
                            1   ing 

  @description              0.. Str Description about location of seat.
                            1   ing 

  Pricing/ParticipantCatego 0.. Str If openAvailability is true,
  ry/TPA\_Extensions/Dynami 1   ing dynamicToken will be Nothing/Empty.
  cToken                            

  Pricing/ParticipantCatego 0..     Contains information about ticket
  ry/TPA\_Extensions/Issue  1       printing.

  @Mandatory                0.. Boo Specifies if the ticket should be
                            1   lea printed by the client.
                                n   

  Pricing/ParticipantCatego 0..     Attributes that we need send between
  ry/TPA\_Extensions/Attrib 1       calls.
  utes                              

  Pricing/ParticipantCatego 0..     Attributes that we need send between
  ry/TPA\_Extensions/Attrib n       calls.
  utes/Attribute                    
  -------------------------------------------------------------------------

|