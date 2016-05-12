---
title: GetRates
keywords: transfers, get rates, rates
sidebar: mydoc_sidebar
permalink: /developer-documentation/transfers/DSF/GetRates
---

|

Method Goals
============

This method aims to retrieve a list of the rates that can be booked.

|

Remarks
=======

|

GetRatesRQ Example
==================

    <GetRatesRQ>
        <timeoutMilliseconds>60000</timeoutMilliseconds>
        <source>
            <languageCode>en</languageCode>
        </source>
        <filterAuditData>
            <registerTransactions>false</registerTransactions>
        </filterAuditData>
        <Configuration codeProvider = "XXXXX">
            <Credentials user = "" password = "">
                <UrlGeneric>http://example.com</UrlGeneric>
            </Credentials>
            <Attributes/>
        </Configuration>
    </GetRatesRQ>

|

GetRatesRQ Description
======================

The request just contains the elements of BaseRQ.

  -------------------------------------------------------------------------
  Element     Numbe Type  Description
              r           
  ----------- ----- ----- -------------------------------------------------
  GetRatesRQ  1           Root node.
  -------------------------------------------------------------------------

|

GetRatesRS Example
==================

    <GetRatesRS>
        <auditData>
            <timeStamp>2014-10-30T11:29:11.5564985+00:00</timeStamp>
            <processTimeMilliseconds>0</processTimeMilliseconds>
        </auditData>
        <operationImplemented>true</operationImplemented>
        <Rates>
            <Rate id = "7" name = "OWShuttle"/>
            <Rate id = "6" name = "RT"/>
            <Rate id = "3" name = "Rate1"/>
            <Rate id = "19" name = "RateAudit"/>
            <Rate id = "13" name = "RateAudit"/>
            <Rate id = "4" name = "Rate2"/>
            <Rate id = "15" name = "Comas Privado 5 - 8 RT"/>
            <Rate id = "11" name = "Comas Privado 13 - 20"/>
            <Rate id = "9" name = "Comas Privado 5 - 8"/>
            <Rate id = "8" name = "Comas Privado 1 - 4"/>
            <Rate id = "16" name = "Comas Privado 9 - 12 RT"/>
            <Rate id = "12" name = "Comas Privado 21 - 31"/>
            <Rate id = "17" name = "Comas Privado 13 - 20 RT"/>
            <Rate id = "14" name = "Comas Privado 1 - 4 RT"/>
            <Rate id = "10" name = "Comas Privado 9 - 12"/>
            <Rate id = "18" name = "Comas Privado 21 - 31 RT"/>
        </Rates>
    </GetRatesRS>

|

GetRatesRS Description
======================

  --------------------------------------------------------------------------
  Element      Numb Type Description
               er        
  ------------ ---- ---- ---------------------------------------------------
  GetRatesRS   1         Root node.

  Rates        1         List of rates.

  Rates/Rate   1         

  @id          1    Stri Code of the rate.
                    ng   

  @name        1    Stri Name of the rate.
                    ng   

  TransferType 1         Contains a list of TransferType. Each TransferType
  s                      contains information about the types of transfer
                         that are available for this rate.

  TransferType 1..n      Contains information related to a type of transfer.
  s/TransferTy           
  pe                     

  @id          1    Stri Code of the TransferType.
                    ng   

  @name        1    Stri Name of the TransferType.
                    ng   

  TransferType 1         Contains a list of vehicles included in this
  /Vehicles              TransferType category.

  TransferType 1..n      Contains a vehicle name and its id.
  /Vehicles/Ve           
  hicle                  

  @id          1    Stri Code of the vehicle.
                    ng   

  @name        1    Stri Name of the vehicle.
                    ng   
  --------------------------------------------------------------------------

|