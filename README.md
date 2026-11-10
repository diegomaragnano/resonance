<a name="english"></a>

# Oscillations, Resonance & Noise

🇮🇹 *Versione italiana più sotto* → [**Vai alla versione italiana**](#versione-italiana)

A small collection of interactive animations and one Jupyter notebook about oscillations and resonance: from a free spring, through damping, forcing and resonance, to a particle in a double-well potential driven by noise (stochastic resonance). Everything is plain HTML, with no installation and no build step.

**Live site:** [https://diegomaragnano.github.io/resonance/](https://diegomaragnano.github.io/resonance/)

## Project structure

```
├── index.html            landing page: cards grouped by topic
├── viewer.html           one page that embeds any animation, with a navigation bar
├── style.css             shared style of index and viewer
├── .nojekyll             tells GitHub Pages to serve files as they are
├── README.md             this file
├── animations/           the 7 standalone animations
└── notebooks/
    ├── plots.html        the notebook exported to HTML (what visitors read)
    └── plots.ipynb       the original notebook (download)
```

- **`index.html`** lists everything. Clicking a card opens the animation in the viewer; "Open full screen ↗" opens the raw file with no bar.
- **`viewer.html?demo=<nome>`** shows an animation under a bar with *Index*, the title, *Previous / Next* (following the storyline below) and *Open in new tab*.
- Each animation is a single self-contained file: it works offline and follows the light/dark mode of your device.

## The modules

| Part | Animation | Topic |
|---|---|---|
| 1 | `spring_mass.html` | Free harmonic oscillator |
| 1 | `damped_spring_mass.html` | Damped harmonic oscillator |
| 1 | `spring_resonance.html` | Forced harmonic oscillator, no damping |
| 1 | `resonance_lab.html` | Driven, damped harmonic oscillator |
| 2 | `double_well.html` | Deterministic marble in a double well |
| 2 | `langevin_marble.html` | The same marble with noise |
| 2 | `stochastic_resonance.html` | Rocking double well plus noise |
| – | `notebooks/plots.html` | Static figures for all of the above (text in Italian) |

## Guide to the animations

Most animations have an animated scene (spring or potential) and one or more plots. Sliders update the simulation immediately.

### 1. Free spring-mass system (`spring_mass.html`)
Unforced and undamped motion.
- **Drag the mass** up or down: sets the amplitude $x_0$.
- **Set $f_0$ directly / Set $k$ and $m$**: choose how the natural frequency is defined.
  - $f_0$ *slider* (0.25–2 Hz): sets the frequency directly.
  - $m$ *slider* (0.5–2 kg) and $k$ *slider* (10–75 N/m): set mass and spring constant; the frequency follows from them.
- **Pause / Reset**: stop and resume the motion; restore the initial state.
- **Time in s / Time in periods**: unit of the time axis of the plot.
- **Energy bars**: shows a panel with kinetic and potential energy.
- **Phase portrait**: shows a panel with velocity against position.
- An information box reports the current parameters: the angular frequency $\omega_0$, the frequency $f_0$, and the period $T$.

### 2. Damped spring-mass system (`damped_spring_mass.html`)
Equation $\ddot{x} + 2\gamma \dot{x} + \omega_0^2 x = 0$, damping ratio $\zeta = \gamma/\omega_0$.
- **Drag the handle on the mass** to choose a new starting point.
- **$\omega_0$ slider** (1–6 rad/s): natural frequency. $\gamma$ **slider** (0–8 s⁻¹): damping rate.
- **Under-damped / Critical / Over-damped**: presets that set $\gamma$ to a typical value for each regime. A badge and an information box show the current regime, and quantities that are relevant for that regime.
- **Release from** $x = +1$ m: restarts the motion from a fixed initial displacement.
- **Pause** and **speed** menu (0.25×, 0.5×, 1×).
- Checkboxes:
  - *Ghost trail*: leaves fading copies of the mass.
  - *Equilibrium line*: marks x = 0.
  - *Envelope* $\pm$: decay envelope (available only in the under-damped regime).
  - *Settling band* $\pm 2$%: band within which the motion is considered settled.
  - *Damping force*: shows the force from the damper.
  - *Time in periods* $T_0$: time axis in units of the natural period.
  - *Phase portrait*: shows velocity against position.
  - *Restart on parameter change*: if on, moving a slider restarts the motion; if off, the current position and velocity are kept and the motion continues with the new parameters.
- The colour of the fluid in the damper indicates the damping strength (low to high $\gamma$).

### 3. Forced undamped system (`spring_resonance.html`)
Equation $m \ddot{x} + k x = F_0 cos(\omega t)$, with $m$ = 1 kg, $k$ = 4 N/m (so $\omega_0$ = 2 rad/s), starting at rest.
- **Pause/Play** and **Restart**.
- **Speed** menu: 1×, 2×, 4×.
- **$\omega/\omega_0$ slider** (0.5–1.5): ratio of the driving frequency to the natural one. Near 1 you see resonance (steady growth); slightly away from 1, beating.
- $F_0$ **slider** (0.2–1.2 N): amplitude of the driving force.
- Checkboxes:
  - *Envelope*: draws the amplitude envelope.
  - *Support motion* $y(t)$: shows how the support moves (exaggerated in the scene).
  - *Phase portrait* $x–\dot{x}$: shows velocity against position.
  - *Auto-restart*: restarts the run automatically after it ends.
- A status line describes what is happening.

### 4. Resonance lab (`resonance_lab.html`)
Driven, damped oscillator with several linked views: the animated spring, the position trace, the resonance curve and a readout panel.
- **Drive frequency slider**: ratio $\omega/\omega_0$ (0.2–3).
- **Quality factor $Q$ slider**: sets the damping (high $Q$ = light damping). The fluid colour goes from amber (heavy damping) to blue (light damping).
- **Drive amplitude slider**.
- **Drive type**: *Moving support* or *Force on the mass*.
- **Stiffness slider**: natural frequency $\omega_0 = \sqrt{k/m}$, with $m$ = 1.
- **Speed** menu: 0.25× to 16×.
- Buttons:
  - *Snap to* $\omega = \omega_0$: jumps exactly to resonance.
  - $\omega / \omega_0$ = 0.5 and $\omega / \omega_0$ = 2: jump to those ratios.
  - *Sweep through resonance*: automatically sweeps the drive frequency across the resonance.
  - *Stop drive*: switches the driving off so the system decays freely.
  - *Pause*, *Reset*.
  - *Phase portrait*: switches the position panel to a velocity-versus-position view.
  - *Phase panel*: shows or hides a plot of the phase lag against frequency ratio.
- The readout panel displays the main quantities, including $Q$.

### 5. Marble in a double well (`double_well.html`)
Dynamics $\dot{x} = x(a − x^2) = −V'(x)$, with $V(x) = x^4/4 − a x^2/2$.
- **Click or drag on the potential** to drop the marble at that position.
- **$a$ slider** (−1 to 3): changes the shape of the potential. For $a \le 0$ there is a single well; for $a > 0$ two wells appear, with the central point becoming unstable.
- **Pause/Play** and **Reset**.
- The shading marks the basins of attraction; the second plot shows $x(t)$ with dashed lines at the fixed points. A readout reports the current time, position and destination.

### 6. Langevin marble (`langevin_marble.html`)
The same marble with noise: $dx = x(a − x^2) dt + \varepsilon dW$.
- $a$ **slider** (−2 to 3): shape of the potential. $\varepsilon$ **slider** (0.05–1.5): noise strength. **Speed slider** (1–40).
- **Pause/Resume**, **Reset marble**, **Clear histogram**.
- **Trail**: shows the recent path of the marble.
- **Colour bands in $x(t)$**: shades the trajectory plot according to which well the marble is in.
- The scene has two bulbs under the wells: the lit one is the well the marble currently occupies.
- Plots: the potential with the marble, the live trajectory $x(t)$ (last 100 time units), and a histogram of where the marble has spent its time, compared with the exact stationary density (red curve). The counter shows time, position and number of jumps between wells.

### 7. Stochastic resonance (`stochastic_resonance.html`)
Rocking double well with noise (Benzi, Sutera & Vulpiani, 1981): $dx = [x(a − x^2) + A \cos \Omega t] dt + \varepsilon dW$.
- Sliders: $a$ (well shape), $A$ (forcing amplitude), $\Omega$ (forcing frequency), $\varepsilon$ (noise), **speed**, and **tilt display** (changes only how strongly the tilt is drawn, not the dynamics).
- **Pause**, **Reset**, and **Colour bands in $x(t)$**.
- **Presets**: *too little noise*, *resonance* and *too much noise* set $\varepsilon$ relative to the optimal value.
- The information panel shows: the threshold forcing $A_c$ (below it the marble cannot cross without noise), the mean exit time compared with half the forcing period, the paper's resonance window for $\varepsilon$, the optimal noise level, and the lock-in response (how much of the ideal switching amplitude the marble achieves), with a bar.
- Plots: the tilted potential with the marble and a gold marker of the forcing phase; $x(t)$ over the last three periods with the signal as a dashed green line; a histogram of residence times between jumps, in units of half a period.

## Notebook

`notebooks/plots.html` contains the code and figures: free, damped, beating, forced and resonant oscillators, Langevin dynamics, the tilted double well and the stochastic simulation. The text of the notebook is in Italian. The original `.ipynb` can be downloaded from the index.

---

<a name="versione-italiana"></a>

# Oscillazioni, risonanza e rumore

🇬🇧 [**Back to the English version**](#english)

Una piccola raccolta di animazioni interattive e di un notebook Jupyter sugli oscillatori: dal sistema massa-molla libero, passando per smorzamento, forzante e risonanza, fino a una biglia in un potenziale a doppia buca guidata dal rumore (risonanza stocastica). Solo HTML, niente installazioni o fasi di compilazione.

**Sito online:** [https://diegomaragnano.github.io/resonance/](https://diegomaragnano.github.io/resonance/)

## Struttura del progetto

```
├── index.html            pagina iniziale: schede raggruppate per argomento
├── viewer.html           una pagina valida per tutte le animazioni, con barra di navigazione
├── style.css             stile condiviso di index e viewer
├── .nojekyll             dice a GitHub Pages di servire i file così come sono
├── README.md             questo file
├── animations/           le 7 animazioni indipendenti
└── notebooks/
    ├── plots.html        il notebook esportato in HTML (quello che vedono gli utenti)
    └── plots.ipynb       il notebook originale (da scaricare)
```

- **`index.html`** elenca tutto. Cliccando una scheda, l'animazione si apre nel viewer; "Open full screen ↗" apre il file puro, senza barra.
- **`viewer.html?demo=<nome>`** mostra un'animazione sotto una barra con *Index*, il titolo, *Previous / Next* (che seguono il percorso qui sotto) e *Open in new tab*.
- Ogni animazione è un singolo file autonomo: funziona anche offline e segue la modalità chiara/scura del dispositivo.

## I moduli

| Parte | Animazione | Argomento |
|---|---|---|
| 1 | `spring_mass.html` | Oscillatore armonico libero|
| 1 | `damped_spring_mass.html` | Oscillatore armonico smorzato |
| 1 | `spring_resonance.html` | Oscillatore armonico forzato, senza smorzamento |
| 1 | `resonance_lab.html` | Oscillatore armonico forzato e smorzato |
| 2 | `double_well.html` | Biglia deterministica in una doppia buca |
| 2 | `langevin_marble.html` | La stessa biglia con il rumore |
| 2 | `stochastic_resonance.html` | Doppia buca oscillante più rumore |
| – | `notebooks/plots.html` | Figure statiche di tutto quanto sopra (testo in italiano) |

## Guida alle animazioni

La maggior parte delle animazioni ha una scena animata (molla o potenziale) e uno o più grafici. Gli slider aggiornano subito la simulazione.

### 1. Sistema massa-molla libero (`spring_mass.html`)
Moto libero e non smorzato.
- **Trascina la massa** in su o in giù: imposta l'ampiezza x₀.
- **Set** $f_0$ **directly / Set** $k$ **and** $m$: sceglie come definire la frequenza naturale.
  - *Slider* $f_0$ (0.25–2 Hz): imposta direttamente la frequenza.
  - *Slider* $m$ (0.5–2 kg) e *slider* $k$ (10–75 N/m): impostano massa e costante elastica; la frequenza ne deriva.
- **Pause / Reset**: ferma e riprende il moto; ripristina lo stato iniziale.
- **Time in s / Time in periods**: unità dell'asse temporale del grafico.
- **Energy bars**: mostra un pannello con energia cinetica e potenziale.
- **Phase portrait**: mostra un pannello con velocità in funzione della posizione.
- Un riquadro informativo riporta i parametri correnti: la frequenza angolare $\omega_0$, la frequenza $f_0$ e il periodo $T$.

### 2. Sistema massa-molla smorzato (`damped_spring_mass.html`)
Equazione $\ddot{x} + 2\gamma \dot{x} + \omega_0^2 x = 0$, rapporto di smorzamento $\zeta = \gamma/\omega_0$.
- **Trascina la maniglia sulla massa** per scegliere un nuovo punto di partenza.
- **Slider** $\omega_0$ (1–6 rad/s): frequenza naturale. **Slider** $\gamma$ (0–8 s⁻¹): coefficiente di smorzamento.
- **Under-damped / Critical / Over-damped**: preset che impostano $\gamma$ a un valore tipico per ciascun regime. Un'etichetta e un riquadro informativo mostrano il regime e le grandezze correnti.
- **Release from** $x = +1$ m: fa ripartire il moto da uno spostamento iniziale fissato.
- **Pause** e menu della **velocità** (0,25×, 0,5×, 1×).
- Caselle di controllo:
  - *Ghost trail*: lascia copie sbiadite della massa.
  - *Equilibrium line*: segna x = 0.
  - *Envelope ±*: inviluppo del decadimento (disponibile solo nel regime sottosmorzato).
  - *Settling band* $\pm 2$%: fascia entro cui il moto si considera assestato.
  - *Damping force*: mostra la forza dello smorzatore.
  - *Time in periods* $T_0$: asse del tempo in unità del periodo naturale.
  - *Phase portrait*: mostra velocità in funzione della posizione.
  - *Restart on parameter change*: se attiva, muovere uno slider fa ripartire il moto; se disattiva, posizione e velocità attuali vengono mantenute e il moto prosegue con i nuovi parametri.
- Il colore del fluido nello smorzatore indica l'intensità dello smorzamento (da $\gamma$ basso a $\gamma$ alto).

### 3. Sistema forzato non smorzato (`spring_resonance.html`)
Equazione $m \ddot{x} + k x = F_0 cos(\omega t)$, con $m$ = 1 kg, $k$ = 4 N/m (quindi $ω_0$ = 2 rad/s), partendo da fermo.
- **Pause/Play** e **Restart**.
- Menu **Speed**: 1×, 2×, 4×.
- **Slider** $\omega / \omega_0$ (0.5–1.5): rapporto tra frequenza forzante e frequenza naturale. Vicino a 1 si osserva la risonanza (crescita continua); poco distante da 1, i battimenti.
- **Slider** $F_0$ (0.2–1.2 N): ampiezza della forza.
- Caselle di controllo:
  - *Envelope*: disegna l'inviluppo dell'ampiezza.
  - *Support motion* $y(t)$: mostra come si muove il supporto (esagerato nella scena).
  - *Phase portrait* $x–\dot{x}$: mostra velocità in funzione della posizione.
  - *Auto-restart*: fa ripartire automaticamente la simulazione al termine.
- Una riga di stato descrive ciò che sta accadendo.

### 4. Resonance lab (`resonance_lab.html`)
Oscillatore forzato e smorzato con più viste collegate: la molla animata, la traccia della posizione, la curva di risonanza e un pannello di valori.
- **Slider Drive frequency**: rapporto $\omega / \omega_0$ (0.2–3).
- **Slider Quality factor** $Q$: imposta lo smorzamento ($Q$ alto = smorzamento debole). Il colore del fluido va dall'ambra (smorzamento forte) al blu (smorzamento debole).
- **Slider Drive amplitude**.
- **Drive type**: *Moving support* (supporto mobile) oppure *Force on the mass* (forza sulla massa).
- **Slider Stiffness**: frequenza naturale $\omega_0 = \sqrt{k/m}$, con $m$ = 1.
- Menu **Speed**: da 0,25× a 16×.
- Pulsanti:
  - *Snap to* $\omega = \omega_0$: porta esattamente a risonanza.
  - $\omega / \omega_0$ = 0.5 e $\omega / \omega_0$ = 2: portano a quei rapporti.
  - *Sweep through resonance*: fa scorrere automaticamente la frequenza forzante attraverso la risonanza.
  - *Stop drive*: spegne la forzante e il sistema decade liberamente.
  - *Pause*, *Reset*.
  - *Phase portrait*: trasforma il pannello della posizione in una vista velocità-posizione.
  - *Phase panel*: mostra o nasconde il grafico dello sfasamento in funzione del rapporto di frequenza.
- Il pannello dei valori mostra le grandezze principali, tra cui $Q$.

### 5. Pallina in una doppia buca (`double_well.html`)
Dinamica $\dot{x} = x(a − x^2) = −V'(x)$, con $V(x) = x^4/4 − a x^2/2$.
- **Clicca o trascina sul potenziale** per lasciar cadere la pallina in quella posizione.
- **Slider** $a$ (da −1 a 3): cambia la forma del potenziale. Per $a \le 0$ c'è una sola buca; per $a > 0$ compaiono due buche e il punto centrale diventa instabile.
- **Pause/Play** e **Reset**.
- L'ombreggiatura segna i bacini di attrazione; il secondo grafico mostra $x(t)$ con linee tratteggiate nei punti fissi. Un'indicazione riporta tempo, posizione e destinazione correnti.

### 6. Pallina di Langevin (`langevin_marble.html`)
La stessa pallina con il rumore: $dx = x(a − x^2) dt + \varepsilon dW$.
- **Slider** $a$ (da −2 a 3): forma del potenziale. **Slider** $\varepsilon$ (0.05–1.5): intensità del rumore. **Slider speed** (1–40).
- **Pause/Resume**, **Reset marble**, **Clear histogram**.
- **Trail**: mostra il percorso recente della pallina.
- **Colour bands in** $x(t)$: colora il grafico della traiettoria a seconda della buca in cui si trova la pallina.
- La scena ha due lampadine sotto le buche: è accesa quella della buca occupata dalla pallina.
- Grafici: il potenziale con la pallina, la traiettoria $x(t)$ in tempo reale (ultime 100 unità di tempo) e un istogramma del tempo trascorso dalla pallina in ciascuna posizione, confrontato con la densità stazionaria esatta (curva rossa). Il contatore mostra tempo, posizione e numero di salti tra le buche.

### 7. Risonanza stocastica (`stochastic_resonance.html`)
Doppia buca oscillante con rumore (Benzi, Sutera e Vulpiani, 1981): $dx = [x(a − x^2) + A cos \Omega t] dt + ε dW$.
- Slider: $a$ (forma delle buche), $A$ (ampiezza della forzante), $\Omega$ (frequenza della forzante), $\varepsilon$ (rumore), **speed** e **tilt display** (cambia solo quanto viene disegnata l'inclinazione, non la dinamica).
- **Pause**, **Reset** e **Colour bands in** $x(t)$.
- **Preset**: *too little noise* (troppo poco rumore), *resonance* e *too much noise* (troppo rumore) impostano $\varepsilon$ rispetto al valore ottimale.
- Il pannello informativo mostra: la soglia di forzante $A_c$ (sotto di essa la pallina non può attraversare senza rumore), il tempo medio di uscita confrontato con metà periodo della forzante, la finestra di risonanza dell'articolo per $\varepsilon$, il livello ottimale di rumore e la risposta lock-in (quanta parte dell'ampiezza ideale di commutazione la pallina raggiunge), con una barra.
- Grafici: il potenziale inclinato con la pallina e un indicatore dorato della fase della forzante; $x(t)$ sugli ultimi tre periodi con il segnale come linea verde tratteggiata; un istogramma dei tempi di permanenza tra i salti, in unità di mezzo periodo.

## Notebook

`notebooks/plots.html` contiene codice e figure: oscillatori libero, smorzato, battimenti, forzato e in risonanza, dinamica di Langevin, doppia buca inclinata e simulazione stocastica. Il testo del notebook è in italiano. Il file `.ipynb` originale si può scaricare dall'indice.
