# DBMS
22.07.16
Uebung

Probeklausur 2)

Aufgabe 1.a)
creat table stromzaehler(
    idzaehler integer primary key,
    zaehlernummer integer unique,
    idort integer,
    einbaulage varchar,
    einbauJahr date,
    constraint stromzaehlerFS foreign key(IDort) references anschlussort(IDort)
)

Aufgabe 1.b)
creat view offenerechnungen as
select *
from rechnungen natural join kunden
where datumeingang is null

Aufgabe 1.c)
select idzaehler
from stromzaehler natural join zaehlerstaende
where (extract(year from CURRENT_DATE)-einbaujahr) > 20 OR zaehlerstand >= 500000

Aufgabe 1.d)
select COUNT(distinct IDkunde)
from offenerechnungen
group by IDkunde
having count(IDrechnung) > 1

Aufgabe 1.e)
select ort
from kunden
group by ort
having count(*) >= all(
          select count(*)
          from kunden
          group by ort
)

Aufgabe 1.f)
UPDATE Rechnungen SET gesamtsumme = (
          SELECT SUM(betrag)
          FROM Rechnungs_Teile
          WHERE IDrechnung = 555
) WHERE IDrechnung = 555

Aufgabe 1.g)
select IDkunde
from tarife natural join kunde_tarif_zaehler
where tarifname='Schnäppchentarif'
intersect
select IDkunde
from rechnungen
where gesammtsumme <= 100

Aufgabe 1.h)
select IDzaehler,zaehlerstand_neu - zaehlerstand_alt
from (select IDzaehelr, zaehlerstand as zaehlerstand_neu
      from zaehlerstaende
      where datum='2011-01-01') 
      join
      (select IDzaehelr, zaehlerstand as zaehlerstand_alt
      from zaehlersteande
      where datum='2010-01-01')
      using(IDzaehler)

//////////////
select stromzaehler.IDzaehler,z11.zaehlerstand - z10.zaehlerstand
from stromzaehler
join zaehlerstaende as z10 using idzaehler
join zaehlerstaende as z11 using idzaehler
where z10.datum='2010-01-01' AND z11.datum='2011-01-01'

Aufgabe 4.3)
