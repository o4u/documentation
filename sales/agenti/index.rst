Agenti di vendita
=================

Il modulo ``sale_commission`` permette di definire gli agenti di vendita e le loro provvigioni.

Nella scheda del cliente, nel tab ``Vendite e Acquisti`` è possibile assegnare gli agenti predefiniti per il cliente.

Gli agenti saranno selezionabili anche direttamente nell'ordine di vendita.

Provvigioni
-----------

Ogni agente deve essere associato ad un tipo di provvigione (campo ``Provvigione`` nel tab ``Informazioni agente`` nella scheda dell'agente).

La provvigione può essere calcolata con una percentuale fissa oppure per scaglioni, basarsi sull'import lordo o netto, ed essere liquidata in base alla validazione oppure al pagamento della fattura cliente.

Liquidazione
------------

Sull'agente è anche associato ad un ``periodo liquidazione``: mensile, trimestrale, semestrale o annuale.

Sarà quindi possibile generare le liquidazioni delle provvigioni maturate dagli agenti e generare automaticamente le loro fatture passive.


Provvigioni con formule avanzate
================================

Grazie modulo ``sale_commission_formula`` è possibile definire delle provvigioni calcolate tramite una formula (di tipo ``Formula``).

La formula è scritto in linguaggio ``python`` e può accedere ai campi della riga del documento, che sia un ordine di vendita o una fattura.

Ecco un esempio:

.. code-block:: python

    if line._name == 'sale.order.line':
        partial = (line.price_subtotal / 100)*5
        result = partial + (partial / 100)*10
    if line._name == 'account.invoice.line':
        partial = (line.price_subtotal / 100)*5
        result = partial + (partial / 100)*10

E` possibile utilizzare ``line`` per accedere ai campi della riga.

Bisogna utilizzare ``result`` per ritornare l'importo della provvigione.

In questo esempio si mostra come eventualmente distinguere il comportamento fra le righe dell'ordine di vendita (``sale.order.line``) e quelle della fattura (``account.invoice.line``).

Il calcolo ottiene il 5% del totale della riga e poi un ulteriore 10% al risultato.

Campi
-----

Esempi di campi delle righe dell'ordine di vendita
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

===============  =========
Campo            Etichetta
===============  =========
discount         Sconto (%)
price_subtotal   Totale
price_unit       Prezzo Unitario
product_uom_qty  Quantità
===============  =========

Esempi di campi delle righe della fattura
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

===============  =========
Campo            Etichetta
===============  =========
discount         Sconto (%)
price_subtotal   Totale
price_unit       Prezzo Unitario
quantity         Quantità
===============  =========


Provvigioni su listini
======================

Tramite il modulo ``sale_commission_pricelist`` è possibile associare le provvigioni alle regole di listino (per maggiori informazioni sui listini, si veda la relativa documentazione).

Per attivare i listini andare su

Vendite → Configurazione → Prezzo di Vendita

selezionare ``Prezzi avanzati basati su formule (sconti, margini, arrotondamenti)`` e salvare.

Poi tramite

Vendite → Configurazione → Listini prezzi

negli elementi del listino è possibile impostare una provvigione.

Quindi, se ad esempio si definisci un listino per lo sconto del 10%, è possibile specificare una provvigione specifica quando in fase di vendita viene applicato tale sconto.

Gestione Resposabile di area
============================

Il modulo ``sale_commission_areamanager`` permette di gestire i responsabili di area e le loro provvigioni.

Nella scheda dell'agente è possibile impostare se l'agente è un responsabile di area tramite il checkbox ``E' un Area Manager``.

Per gli agenti sottoposti, è necessario invece riempire il campo ``Area Manager``, selezionando l'agente responsabile dell'agente corrente, e la provvigione da utilizzare per il responsabile quando applicato all'agente corrente.

Nel preventivo, utilizzando un agente che ha anche un responsabile, al salvataggio del preventivo stesso, il responsabile verrà aggiunto fra gli agenti coinvolti e le provvigioni calcolate.