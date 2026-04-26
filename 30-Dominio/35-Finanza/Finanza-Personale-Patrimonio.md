---
tipo: concetto
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - finanza
  - dominio/personale
  - patrimonio
area: finanza
---

# Finanza — Personale — Patrimonio

> [!info] In una frase
> Patrimonio personale oggi: **conto corrente** (unico liquido operativo) + **fondo pensione** (riserva vincolata, riscatto anticipato con haircut). Nessun immobile, nessun portafoglio titoli, nessun asset alternativo.

## Composizione

| Categoria | Presente | Liquidità | Ruolo nella transizione |
|---|---|---|---|
| Conto corrente | ✅ | Piena | **Asset primario** — alimenta il runway |
| Fondo pensione | ✅ | Vincolata (riscatto anticipato con penale) | **Buffer estremo** — solo scenario di transizione critica |
| Beni immobili | ❌ | — | Non applicabile |
| ETF / azioni / obbligazioni | ❌ | — | Non applicabile |
| Crypto / asset alternativi | ❌ | — | Non applicabile |

## Conto corrente

Unico strumento liquido. È il pool che sostiene il [[Finanza-Personale-Runway-Transizione|runway]] dichiarato oggi (12-18 mesi di copertura, al netto dei viveri — vedi [[Finanza-Personale-Flussi]]).

> [!todo] Quantificazione aperta
> Importo esatto del conto corrente non ancora tracciato nel vault. Non strettamente necessario finché l'ordine di grandezza del runway resta confortevole (vedi [[Finanza-Personale-Runway-Transizione]]), ma andrà inserito quando si avvicinerà il T0 di uscita.

## Fondo pensione

Alimentato esclusivamente da **ritenute payroll** sullo stipendio Angelini. **Nessun versamento volontario** in aggiunta.

Regime di riscatto anticipato: in uno scenario di transizione critica è prelevabile, ma **non al 100%** — una quota viene trattenuta dal fondo stesso a titolo di penalizzazione.

**Conseguenze operative**:
1. Il fondo pensione **non entra nel calcolo del runway "pulito"**. È un buffer di riserva, non una leva ordinaria.
2. Al termine del rapporto con Angelini (vedi [[Finanza-Personale-Flussi]]), si fermano automaticamente anche le ritenute pensione → lo strumento smette di crescere.

> [!question] Domanda aperta
> Entità precisa dell'haircut sul riscatto anticipato. Da quantificare se il fondo pensione diventa rilevante come buffer (oggi scenario remoto).

## Cosa non c'è (e perché è rilevante)

L'assenza di immobili, titoli e asset alternativi significa che:
- **Niente rendite passive** da affitto o cedole → [[Finanza-Personale-Flussi|flussi]] dipendono al 100% dallo stipendio.
- **Niente liquidabilità graduata** — il patrimonio è binario: liquido immediato (CC) o vincolato con penale (pensione).
- **Nessun rischio di concentrazione** su asset volatili (ETF/crypto) da gestire in transizione.

Semplicità strutturale: riduce la complessità del calcolo runway, ma toglie leve di ottimizzazione.

## Collegamenti

- [[Finanza-Personale]] · [[Finanza-MOC]]
- [[Finanza-Personale-Flussi]] — come il patrimonio si alimenta e si consuma
- [[Finanza-Personale-Runway-Transizione]] — come il patrimonio sostiene la transizione
- [[Angelini-Pharma]] — fonte unica di alimentazione del patrimonio oggi
