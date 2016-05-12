---
title: GetTransferTypes
keywords: transfers, get transfers, transfers types
sidebar: mydoc_sidebar
permalink: /developer-documentation/transfers/DSF/GetTransferTypes
---

|

Method Goals
============

|

Remarks
=======

|

GetTransferTypesRQ Example
==========================

    <GetTransferTypesRQ>
        <timeoutMilliseconds>60000</timeoutMilliseconds>
        <source>
            <languageCode>en</languageCode>
        </source>
        <filterAuditData>
            <registerTransactions>false</registerTransactions>
        </filterAuditData>
        <Configuration codeProvider = "XXXXX">
            <Credentials user = "" password = "">
                <UrlGeneric>http://examples.com</UrlGeneric>
            </Credentials>
            <Attributes/>
        </Configuration>
    </GetTransferTypesRQ>

|

GetTransferTypesRQ Description
==============================

  -------------------------------------------------------------------------
  Element     Numbe Type  Description
              r           
  ----------- ----- ----- -------------------------------------------------
  GetTransfer 1           Root node.
  TypesRQ                 
  -------------------------------------------------------------------------

|

GetTransferTypesRS Example
==========================

    <GetTransferTypesRS>
        <auditData>
            <timeStamp>2014-10-30T11:35:31.1499128+00:00</timeStamp>
            <processTimeMilliseconds>0</processTimeMilliseconds>
        </auditData>
        <operationImplemented>true</operationImplemented>
        <TransferTypes>
            <TransferType id = "15" name = "Privado - 9 - 12 Personas"/>
            <TransferType id = "3" name = "Compartido - Shuttle Express"/>
            <TransferType id = "2" name = "Compartido - Shuttle"/>
            <TransferType id = "16" name = "Privado - 13 - 20 Personas"/>
            <TransferType id = "17" name = "Privado - 21 - 31 Personas"/>
            <TransferType id = "13" name = "Privado - 1 - 4 Personas"/>
            <TransferType id = "14" name = "Privado - 5 - 8 Personas"/>
            <TransferType id = "5" name = "Privado - VIP"/>
        </TransferTypes>
    </GetTransferTypesRS>

|

GetTransferTypesRS Description
==============================

  -------------------------------------------------------------------------
  Element     Numbe Type  Description
              r           
  ----------- ----- ----- -------------------------------------------------
  GetSupplmen 1           Root node.
  etsRS                   

  TransferTyp 1           List of transfers types.
  es                      

  TransfersTy 1           Type of transfer
  pes/                    
  TransfersTy             
  pe                      

  @id         1     Strin Code of the supplement. Sole codes.
                    g     

  @name       1     Strin Name of the supplement.
                    g     
  -------------------------------------------------------------------------

|