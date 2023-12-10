# Bazy-Danych-Projekt-2023/2024

<img src="./agh_logo.png">

<h2 style="text-align: center;">Systemy Baz Danych 2023/2024
– projekt
systemu bazodanowego dla firmy oferującej
kursy i szkolenia </h2>

**Autorzy**:
<div > 
    <p style="text-align: left;">
    Piotr Śmiałek <br> 					
    Robert Zuziak<br>
    Hubert Tułacz<br>
    </p>
 </div>

**Prowadzący**						
<div> 
<p>
 dr inż. Robert Marcjan
 </p>
</div>


<h3>Funkcje użytkowników</h3>

**Użytkownik anonimowy (gość):**
- Przeglądanie dostępnych webinariów.
- Przeglądanie dostępnych kursów.
- Przeglądanie dostępnych studiów.
- Przeglądanie dostępnych informacji o wykładowcach.
- Przeglądanie dostępnych terminów i miejsc spotkań stacjonarnych.
- Rejestracja na darmowe webinaria.
- Przeglądanie nagrań webinariów dostępnych publicznie.
- Możliwość założenia konta

**Użytkownik zarejestrowany:**
- Logowanie do systemu.
- Przeglądanie dostępnych webinariów.
- Przeglądanie kursów.
- Przeglądanie studiów.
- Przeglądanie informacji o wykładowcach.
- Rejestracja na płatne webinaria.
- Zapisywanie się na kursy (wybór terminów i formy zajęć).
- Zapisywanie się na studia (wybór specjalizacji).
- Przeglądanie własnych zapisów i historii uczestnictwa.
- Przeglądanie informacji o płatnościach.
- Odrabianie nieobecności na zajęciach (jeśli to możliwe).


**Wykładowca/Nauczyciel:**

Zarządzanie Kursami/Spotkaniami:

- Dodawanie nowych kursów, webinarów i studiów do systemu.
- Zarządzanie terminami i miejscami spotkań stacjonarnych.
- Aktualizacja informacji o programach nauczania (sylabusach).
- Przypisywanie uczestników do kursów i studiów.

 Zarządzanie Ocenami i Frekwencją:

- Wprowadzanie ocen dla uczestników kursów.
- Zaznaczanie obecności na spotkaniach stacjonarnych i online.
- Generowanie raportów dotyczących frekwencji i ocen.

**Administrator systemu:**
- Dodawanie, edytowanie i usuwanie webinariów.
- Dodawanie, edytowanie i usuwanie kursów.
- Dodawanie, edytowanie i usuwanie studiów.
- Zarządzanie listą wykładowców.
- Zarządzanie terminami i miejscami spotkań stacjonarnych.
- Zarządzanie użytkownikami (edycja danych, blokowanie, usuwanie).
- Przeglądanie raportów finansowych.
- Generowanie listy "dłużników".
- Generowanie raportu dotyczącego liczby zapisanych osób na przyszłe wydarzenia.
- Generowanie raportu dotyczącego frekwencji na zakończonych wydarzeniach.
- Generowanie listy obecności dla każdego szkolenia.
- Generowanie raportu bilokacji.
- Zarządzanie rolami i uprawnieniami użytkowników.
- Dodawanie nowych użytkowników.
- Edycja treści i opisów kursów, studiów, webinariów.


<img src="./schemat_bazy_danych.png">

<h3>Tabele: </h3>

**Users** - tabela zawiera wszystkich użytkowników w systemie (studentów i pracowników)
- UserID (PK)- Identyfikator użytkownika 
- Firstname - imię użytkownika
- LastName - nazwisko użytkownika
- Address - adres użytkownika
- Email - email użytkownika
- Password - hasło użytkownika


		
**Employees** -zawiera pracowników z przydzieloną rolą pracownik/administrator
- UserID (Fk) - identyfikator w tabeli Users
- Role - rola, admin/teacher/tłumacz

**Students** - tabela zawiera tylko studentów z tabeli Users 
- UserID - Identyfikator w tabeli Users
	     

**Shopping Cart** - tabela zawierające informacje o koszyku dla każdego studenta
- CartID (PK) - klucz główny koszyka
- RegistrationID - identyfikator rejestracji z której pochodzi stanowisko w koszyku
- UserID - identyfikator użytkownika do którego należy koszyk
- TransactionStatus - czy koszyk został już opłacony
- TransactionDate - data do której koszyk ma być zrealizowany

**Pending** - tabela zawierająca informacje o poszczególnych wpłatach w ramach koszyka (wpisowe, opłaty z zjazd)
- CartID - identyfikator koszyka z którego pochodzą poszczególne opłaty
- RegistrationID - identyfikator rejestracji z której pochodzą poszczególne opłaty
- DueDate - data do której dana należność ma być uregulowana
- Price - wartość należności

**Courses** - zawiera kursy oraz informacje o nich
- CoursesID (Pk) - klucz główny kursu
- Name - nazwa
- Description - tekstowy opis kursu
- Prepayment - zaliczka przy zapisie
- Full Payment - dopłata całości kwoty (z wyłączeniem zaliczki)
- CourseStartDate - data rozpoczęcia kursu
- Type - zdalny/online synchroniczny/online asynchroniczny/hybrydowy
- NumberOfSeats - liczba miejsc na kurs
- Language - język w jakim jest prowadzony kurs


**Registration** - tabela zawiera rejestracje dla każdego studenta. Student może mieć wiele rejestracji (może uczęszczać na wiele eventów)
- RegistrationID (PK) - identyfikator rejestracji	
- EventType - rodzaj wydarzenia na który zapisał się student
- EventID - identyfikator wydarzenia
- UserID (PK)- Identyfikator użytkownika
- RegistrationDate - data zarejestrowania na dane wydarzenie
- Attendance - procentowa wartość obecności na danym wydarzeniu
- Status - czy student zakończył, jest w trakcie lub nie ukończył wydarzenia
	
	


**CourseMeetings** - zawiera wszystkie spotkania w ramach jednego kursu
- MeetingID - klucz główny identyfikator każdego spotkania
- CourseID - identyfikator kursu do którego należy spotkanie
- TeacherID - identyfikator nauczyciela prowadzącego spotkanie
- Room - sala w jakiej odbywa się spotkanie
- StartDateAndTime - data i godzina odbycia się zajęć
- Type - czy spotkanie jest stacjonarne/zdalne/zdalnie asynchronicznie
- Link - link do zewnętrznego komunikatora (jeżeli stacjonarnie to NULL)

**CourseAttendance** - Zawiera informacje o obecności studenta na zajęciach kursu
- MeetingID - identyfikator kursu
- UserID - identyfikator studenta
		

**Internships** - zawiera informacje o praktykach studentów
- InternshipID - klucz główny identyfikatora praktyki 
- StudiumID - identyfikator studiów do których częścią jest dana praktyka
- RegistrationID - identyfikator rejestracji na dane praktyki
- StartDate - data rozpoczęcia praktyk
- EndDate - data zakończenia praktyk
- AttendanceDays - liczba dni na których student był obecy (od 0 do 14)
- ExamGrade - ocena z egzaminu

 
**Webinarium** - tabela zawierająca wszystkie webinary w systemie
- WebinarID (PK) - identyfikator webinaru
- TeacherID (FK) - identyfikator nauczyciela prowadzącego zajęcia
- TranslatorID (FK) - identyfikator tłumacza
- Name - nazwa webinaru
- Descryption - opis webinaru
- Price - cena webinaru (jeśli free to 0)
- Type (free or not) - darmowy czy płatny
- Link (to external website) - link do webinaru
- StartDateAndTime - dokładna data starru webinaru
- ExpirationDate - data wygaśnięcia webinaru
- WebinariumDuration - czas trwania webinaru




**WebinarAttendance** - tabela zawierająca informacje o użytkownikach obecnych na webinarze
- MeetingID (FK) - identyfikator webinaru
- UserID (FK) - identyfikator uzytkownika


**StudyMeetings** - Zawiera informacje o zajęciach w ramach jednego kierunku
- StudyMeetingsID - Identyfikator spotkania
- GatheringID (FK) - identyfikator zjazdu
- TeacherID (FK) - identyfikator nauczyciela prowadzącego zajęcia
- TranslatorID (FK) - identyfikator tłumacza
- Room - numer sali w której odbywają się zajęcia
- StartDateAndTime - data i godzina o której odbędą się zajęcia
- Type - typ stacjonarne/zdalne/zdalne asynchroniczne
- Link - link do zewnętrznego komunikatora (jeżeli stacjonarne to NULL)
- StudyMeetingPrice - koszt zjazdu
- StudyMeetingDuration - czas trwania spotkania
		


**StudyAttendance** - Zawiera informacje o obecności studenta na zajęciach na studiach
- MeetingID - identyfikator webinaru
- UserID - identyfikator studenta


**Studies** - zawiera informacje dotyczące kierunków studiów
- StudiumID - klucz główny identyfikatora studiów
- Name - nazwa kierunku
- Syllabus - opis studiów
- NumberOfSeats - liczba miejsc na dany kierunek
- EntryFee - wpisowe na studia
- Language - język w jakim prowadzone są studia

**Gatherings** - zjazdy w ramach jednego kierunku studiów
- GatheringID (Pk) - identyfikator zjazdu
- StudiumID (FK) - identyfikator studiów 
- GatheringPrice - cena zjazdu
- GatheringDate - data zjazdu


