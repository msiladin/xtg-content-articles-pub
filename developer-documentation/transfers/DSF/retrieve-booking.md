---
title: RetrieveBooking
keywords: transfers, retrieve booking
sidebar: mydoc_sidebar
permalink: /developer-documentation/transfers/DSF/retrieve-booking
---

|

Method Goals
============

This method aims to Retrieve Booking details.

|

RetrieveBookingRQ Example
=========================

:

    <RetrieveBookingRQ>
        <timeoutMilliseconds>60000</timeoutMilliseconds>
        <source>
            <agencyCode>xxxx</agencyCode>
            <languageCode>es</languageCode>
        </source>
        <filterAuditData>
            <registerTransactions>true</registerTransactions>
        </filterAuditData>
        <Configuration codeProvider = "XXX">
            <Credentials user = "XXX" password = "XXX">
                <UrlGeneric>XXX</UrlGeneric>
                <UrlIdentification xsi:nil = "true"/>
                <UrlAvailability xsi:nil = "true"/>
                <UrlRateRule xsi:nil = "true"/>
                <UrlRetrieveBooking xsi:nil = "true"/>
                <UrlsSpecific xsi:nil = "true"/>
            </Credentials>
            <Attributes>
            </Attributes>
        </Configuration>
        <Locator id = "XXX" type = "PROVIDER"/>
    </RetrieveBookingRQ>

|

RetrieveBookingRQ Description
=============================

The request format works the same way as the Book response. the main
difference is that only contains the locator of the provider's system.

  ------------------------------------------------------------------------
  Element           Numbe Type     Description
                    r              
  ----------------- ----- -------- ---------------------------------------
  RetrieveBookingRQ 1              Root Node

  RetrieveBookingRQ 1     Locator  Contains the locator of the provider's
  /Locator                         system.

  RetrieveBookingRQ 1     String   The code that's identifies the
  /Locator/id                      reservation in the provider's system.

  RetrieveBookingRQ 1     eLocator Indicates the type of the locator. The
  /Locator/type           Type     possible values are: **PROVIDER**.
  ------------------------------------------------------------------------

|

RetrieveBookingRS Example
=========================

:

    <RetrieveBookingRS>   
        <auditData>
            <transactions>
                <timeStamp>2014-09-19T13:44:18.716787+01:00</timeStamp>
                <RQ></RQ>
                <RS></RS>
            </transactions>
            <timeStamp>2014-10-11T14:52:17.2162683+01:00</timeStamp>
            <processTimeMilliseconds>0</processTimeMilliseconds>
        </auditData>
        <operationImplemented>true</operationImplemented>
        <SelectedRates>
            <SelectedRate id = "0" rateType = "OW">
                <SelectedOptions>
                    <SelectedOption status = "CONFIRMED" id = "0">
                        <Transfers>
                            <Transfer id = "0">
                                <Info type = "BUS" code = "XXX" typeVeh = "XXX">
                                    <vendorMessages>
                                        <vendorMessage>
                                            <Tittle>XXX</Tittle>
                                            XXXXXXXXXXXXXXXXXXXXXX
                                        </vendorMessage>
                                    </vendorMessages>
                                </Info>
                                <LocOrigin type = "ARP" code = "PMI" date = "2014-09-19T00:00:00"/>
                                <LocDestination type = "HOT" code = "XXX" date = "2014-09-19T00:00:00"/>
                            </Transfer>
                        </Transfers>
                        <Parameters></Parameters>
                    </SelectedOption>
                </SelectedOptions>
                <TotalRate currency = "EUR" amount = "5.350" priceType = "NET" commission = "0.640"/>
            </SelectedRate>
            <SelectedRate id = "1" rateType = "OW">
                <SelectedOptions>
                    <SelectedOption status = "CONFIRMED" id = "1">
                        <Transfers>
                            <Transfer id = "1">
                                <Info type = "BUS" code = "XXX" typeVeh = "XXX">
                                    <vendorMessages>
                                        <vendorMessage>
                                            <Tittle>XXXX</Tittle>
                                            XXXXXXXXXX
                                        </vendorMessage>
                                    </vendorMessages>
                                </Info>
                                <LocOrigin type = "ARP" code = "XXX" date = "2014-09-19T00:00:00"/>
                                <LocDestination type = "HOT" code = "XXX" date = "2014-09-19T00:00:00"/>
                            </Transfer>
                        </Transfers>
                        <Parameters></Parameters>
                    </SelectedOption>
                </SelectedOptions>
                <TotalRate currency = "EUR" amount = "5.350" priceType = "NET" commission = "0.640"/>
                <CancellationPolicy/>
            </SelectedRate>
        </SelectedRates>
        <ReservationStatus>RESERVED</ReservationStatus>
        <Warnings> 
            <Warning>
                …
            </Warning>   
            . . .
        </Warnings> 
        <Errors> 
            <Error>
                …
            </Error>
            . . .    
        </Errors>
    </RetrieveBookingRS>

|

RetrieveBookingRS Description
=============================

The response format works the same way as the RateRule reponse. The main
difference is that we return the ReservationStatus.

  -------------------------------------------------------------------------
  Element           Numb Type        Description
                    er               
  ----------------- ---- ----------- --------------------------------------
  RetrieveBookingRS 1                Root Node

  RetrieveBookingRS 1    Locator     Contains the locator of the provider's
  /Locator                           system.

  RetrieveBookingRS 1    SelectedRat Contains a list of the selectedRates
  /SelectedRates         es          booked.

  RetrieveBookingRS 1    eTransactio The possible values are:
  /ReservationStatu      nStatusType **UNSUCCESSFUL**; **REQUESTED**;
  s                                  **RESERVED**; **CANCELLED**
  -------------------------------------------------------------------------

|