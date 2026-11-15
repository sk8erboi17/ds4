# Regole per le modifiche

Leggere anche `AGENT.md`: le sue istruzioni restano applicabili.

## Dimostrazioni obbligatorie prima dei commit

Prima di creare **ogni commit**, dimostrare con Vampire gli obblighi formali
pertinenti alla modifica. Usare il prover locale
`tools/vampire/cmake-build/vampire`; conservarne versione e SHA-256.

- Collegare ogni obbligo al frammento di sorgente e alla relativa specifica.
  Conservare gli input TPTP, gli hash dei sorgenti, i comandi esatti e le prove
  TSTP complete in un registro riproducibile locale sotto `proofs/vampire/`.
  PDF, materiale Vampire e test aggiunti restano locali e ignorati da Git;
  non aggiungerli ai commit. I test ereditati dalla base restano versionati.
- Contare come dimostrato soltanto un obbligo con esito `SZS status Theorem`
  o una refutazione `Unsatisfiable` dell'obbligo negato, con prova prodotta.
  Timeout, esaurimento delle risorse, `Unknown` e assenza di controesempi non
  valgono come prova. Verificare le ipotesi e distinguere i lemmi matematici
  dalla correttezza del programma C/Metal che li usa.
- Non assumere come assioma la proprietà da dimostrare, né un suo equivalente.
  Elencare i contratti esterni e gli eventuali collegamenti al codice ancora
  aperti. Aggiungere controlli negativi pertinenti e verificare che siano rilevati.
- Se gli obblighi necessari del commit restano aperti, continuare il lavoro e
  non creare quel commit. Non rimuovere una correzione soltanto perché il
  prover non riesce a chiudere una query.
- Eseguire anche build e regressioni appropriate: la prova logica non verifica
  da sola compilatore, driver o prestazioni. Registrare nel registro locale
  il commit, gli hash dei sorgenti e l'ambito delle prove.

Eseguire i prover in serie, con un solo core e priorità bassa, entro i limiti
di memoria e tempo della sessione. Non avviare modelli o inferenza pesante senza
autorizzazione dell'utente. Non copiare i GGUF: usare collegamenti simbolici.
