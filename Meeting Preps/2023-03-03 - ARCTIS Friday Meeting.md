## Topics
- [ ] Strategie für das Meeting mit TUM
      - ==*(Prof. Yavrukuc hat inzwischen zugesagt)*==   
      - ==*Was müssen wir alles bis dahin vorbereiten?*==
	- [ ] Was müssen wir bis 30.04 alles abgeben?
		- [ ] **Status Review**
		      ==*Ist das ein extra Dokument oder gehört das zu dem fachlichen Zwischenbericht?*==
		- [ ] **Fachlicher Zwischenbericht in profi-online**
		      ==*Wo ist der Link zu profi-online?*==
		      ==*Wie ist der Bericht aufgebaut (wer soll was schreiben)?*==
			- <u>Stand der aktuell zu bearbeitenden APs</u>
				- HM (Leistungsoptimierte Rotorregelung):
					AP 1.1-Modellbildung Rotor mit Morphing (M1-11 (seit Juni bis Mai?))
					AP 1.2-Extremwertregelung (M5-M17)
				- TUD (Akustik)
					AP 2.1-Aeroakustikmodell (M1-M12)
					AP 2.2-Lärmschätzung (M5-M17)
			- <u>Schnittstellendoku</u>
			  *==(mit TUM besprechen)==*
			- <u>Dokumentieren wer was gemacht hat</u>
			  *==(mit TUM besprechen)==*
		- [ ] **Rechnerischer Zwischenbericht (von ADM auszuführen)**
- [ ] Lifting


## Lifting
The time lifted transfer operator $\hat{H}(z)$ in a state-space setting ([[@(bittanti2009a)_Periodic Systems|bittanti2009a]])
$$\begin{array}{r}
x(kT+T)=Fx(kT)+Gu_{k}\\
y_k=H_kx(kT)+Eu_k
\end{array}$$
where $F=\Psi_{A}(T,0)$ (the [[Floquet Theory and Stability|Monodromy Matrix]]), and:
$$Gu_k=\int_{0}^{T}\Phi_A(T,\tau)B(\tau)\ u(kT+\tau)\ d\tau$$
$$H_k=C(t)\Phi_A(t,0)$$
$$Eu_k=\int_{0}^{t}\left(C(t)\Phi_A(t,\tau)+D(t)\delta(t-\tau)\right)\ u(kT+\tau)\ d\tau$$

>[!Note]+ 
>$x(kT+T) \rightarrow$ The state is only calculated for the beginning of the new period
>$$y_k=C(t)\Phi_{A}(t,\tau)x(\tau)+\int_{\tau}^{t}C(t)\Phi_{A}(t,\sigma)B(\sigma)u(\sigma) d\sigma +D(t)u(t)$$
>or in discrete time:
>$$y(t)=C(t)\Phi_{A}(t,\tau)x(\tau)+\left(\sum\limits_{j=\tau+1}^{t}C(t)\Phi_{A}(t,j)B(j-1)u(j-1)\right)+D(t)u(t)$$



