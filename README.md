# OpenDatalayer Default Model
This repository contains the default model for the OpenDatalayer.

## What is a "model" in the context of the ODL?
A model represents the structural "glue" between the ODL and the embedding website or webapplication. Each model
provides type definitions used for passing data to the ODL. Additionally, it contains a JSON-based mapping
that describes the data that has to be provided per pagetype.

A website that implements the ODL has to obey one specific model (either this default or any custom one) so
the ODL and its tools (e.g. Builder and Validator) know where to expect which kind of data. Think of the model as
a contract between a website and the ODL.

E.g. this model is designed for e-commerce-driven websites (as ODL is originally built and developed within
an e-commerce website) and contains a lot of product- and order-specific types. However, due to the
modular concept it is easily possible to use ODL for any other website by simply using another model.

## What are "types" and which "types" exist in this model?
Because of the non-statically-typed nature of Javascript and JSON the ODL implements several virtual data
types used as a "contract" between any embedding applications and the ODL. The contained information is
based on context (e.g. page, user, search, ...) and not on any business domain.

The ODL datamodel is described using the [AVRO description language](https://avro.apache.org/docs/current/),
this allows for machine processing and automation of validation processes. The full list of type definitions is
located under the `model` directory in this repository. Please point any external links to type definitions
to the respective file in that repository.

### Available data types
* [model/ODLGlobalData.avdl](model/ODLGlobalData.avdl)
* [model/ODLSiteData.avdl](model/ODLSiteData.avdl)
* [model/ODLPageData.avdl](model/ODLPageData.avdl)
* [model/ODLUserData.avdl](model/ODLUserData.avdl)
* [model/ODLBrandData.avdl](model/ODLBrandData.avdl)
* [model/ODLErrorData.avdl](model/ODLErrorData.avdl)
* [model/ODLLoginData.avdl](model/ODLLoginData.avdl)
* [model/ODLRegistrationData.avdl](model/ODLRegistrationData.avdl)
* [model/ODLPriceData.avdl](model/ODLPriceData.avdl)
* [model/ODLCategoryData.avdl](model/ODLCategoryData.avdl)
* [model/ODLNavigationData.avdl](model/ODLNavigationData.avdl)
* [model/ODLSearchData.avdl](model/ODLSearchData.avdl)
* [model/ODLProductData.avdl](model/ODLProductData.avdl)
* [model/ODLCartData.avdl](model/ODLCartData.avdl)
* [ODLCartProductData](#odlcartproductdata)
* [model/ODLOrderData.avdl](model/ODLOrderData.avdl)
* [model/ODLAddressData.avdl](model/ODLAddressData.avdl)
* [model/ODLCustomerData.avdl](model/ODLCustomerData.avdl)
* [ODLMediaData](#odlmediadata)
* [ODLMediaPositionData](#odlmediapositiondata)
* [model/ODLNewsletterData.avdl](model/ODLNewsletterData.avdl)
* [model/ODLPromotionData.avdl](model/ODLPromotionData.avdl)

*TODO: move following parts into Avro model files*

### ODLCartProductData
Describes a single prduct within a shopping basket. Inherits all properties from [ODLProductData](model/ODLProductData.avdl)
and adds a `quantity` attribute.

    ODLCartProductData = extend(ODLProductData, {
      /**
        * Anzahl dieses Artikels im zugehörigen Warenkorb.
        */
      "quantity" : {
        "type" : "int",
        "mandatory" : true
      }
    })

### ODLMediaData
Describes a media item (video, audio).

    ODLMediaData = {
      /**
        * Typ des Medienobjektes (video|audio).
        */
      "type" : {
        "type" : "String",
        "mandatory" : true
      },
      /**
        * Name oder ID des Medienobjektes (einmalig(!); sonst frei wählbar, z.B. Dateiname).
        */
      "id" : {
        "type" : "String",
        "mandatory" : true
      },
      /**
        * Vollständige URL zu Mediadatei.
        */
      "url" : {
        "type" : "String",
        "mandatory" : true
      },
      /**
        * Abspieldauer in Sekunden.
        */
      "duration" : {
        "type" : "int",
        "mandatory" : true
      },
    }

### ODLMediaPositionData
Describes a certain position withina media object and is used e.g. for this position
tracking of video and audio data.


    ODLMediaPositionData = {
      /**
        * ID des Medienobjektes, das dieses Event auslöst.
        */
      "id" : {
        "type" : "String",
        "mandatory" : true
      },
      /**
        * Zu übermittelnde Position im Medienobjekt.
        */
      "position" : {
        "type" : "int",
        "mandatory" : true
      }
    }
