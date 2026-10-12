# Consulter un financement

Utilisez la section **Funds** d’un projet pour voir ses financements. Elle apparaît si vous avez le droit de consulter les financements de ce projet. Le guide React ne comporte pas de fiche de financement distincte.

## Trouver le financement

Ouvrez le projet, puis choisissez **Funds**. Vérifiez le financeur, l’institution gestionnaire, la période et la référence pour repérer la bonne ligne. Le tableau affiche aussi **Budgeted**, **Net expense**, **Available** et le statut du financement. Par exemple, ORION — Optical Resilience présente `DM-ORION-BRIDGE` ainsi qu’un autre financement. Sélectionnez la ligne voulue pour ouvrir son aperçu financier et ses dépenses individuelles sous la liste.

<figure class="lm-screenshot" markdown>
![Section Funds d’ORION avec deux financements, leurs périodes et les colonnes financières](../../assets/screenshots/finance/project-funds.png)
</figure>

Pour chercher dans plusieurs projets, utilisez plutôt l’[Explorateur de fonds](fund-explorer.md). Ses lignes représentent des postes de financement : un même financement peut donc apparaître plusieurs fois.

## Lire l’aperçu financier

**Financial overview** regroupe les postes de financement et les postes de dépense par type de coût. Lisez la ligne de total pour connaître le montant, la dépense nette et le solde disponible affichés. La vue du financement `DM-ORION-BRIDGE` sélectionné présente ces totaux sous les lignes de types de coût. La dépense nette peut porter un signe moins dans cette synthèse ; les transactions individuelles apparaissent dans la liste des dépenses. Utilisez-la pour examiner les opérations derrière le total. **Available** est le solde affiché par LabsManager pour les données actuelles, pas une prévision des engagements futurs.

<figure class="lm-screenshot" markdown>
![Aperçu financier du financement relais d’ORION, regroupé par type de coût avec les totaux](../../assets/screenshots/finance/fund-overview.png)
</figure>

La ligne du financement affiche aussi sa date de fin. Pour comparer les échéances des financements visibles, ouvrez Fund explorer et triez sur **End date**. Ce parcours ne propose pas de vue « bientôt terminé » dédiée.

## Si des informations manquent

La section **Funds** et ses actions dépendent des droits. Si elle est absente, demandez à un administrateur du laboratoire l’accès au projet et à ses financements. Si un financement est visible mais sans ligne de dépense, il peut simplement ne comporter aucune dépense visible ; ne déduisez pas un solde nul de cette liste vide sans vérifier l’aperçu.

Pour les budgets du projet et les transactions individuelles, poursuivez avec [Budgets et dépenses](budgets-and-expenses.md).
