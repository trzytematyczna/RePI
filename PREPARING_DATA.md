
0. wybranie podzbioru konferencji
1. Create_tables.sql
	I. stworzenie tabeli trustcom_papers zawierajacej: 
		(i) wszystkie papiery z selected conferences 
		(ii) wszystkie papiery ktore cytuja selected conferences 
		(iii) wszystkie papiery cytowane przez selected conferences
	II. stworzenie tabeli trustcom_paperreferences zawierajacej:
		(i) reference papierow z trustcom_papers
		(ii) pomniejszone o papiery ktore sa usuniete z papers
		(iii) usuniecie powtarzajacych sie par
2. trustcom_print_timeseries.sql <- wewnetrzne wywolanie trustcom_timeseries_fn.sql
3. from copy_conference_first_publication_year.sql --> stowrzenie pliku wykorzysytywanego w citationratios.R

copy (
		select min(year), normalized_venue from trustcom_papers where  normalized_venue in
			('cvpr','ijcv','icra','iccv','icml','nips','jmlr','acl','taslp','emnlp','aaai','tfs','dss','prl','aamas','ijcai','cviu','neural networks','icpr','ieee transactions on neural networks','ijar','nc','bmvc','computer speech language','international journal of applied evolutionary computation','gecco','cl','coling','ieee transactions on affective computing','jair','kr','nca','icdar','ijcnn','aim','icaps','ecai','colt','ijis','jar','ijdar','ci','tap','eccv','natural language engineering','uai','npl','machine translation','icb','alt','paa','ictai','naacl','nca','accv','dss','iccbr','ijprai','wias','ida','ilp','jetai','tslp','pricai','ksem','ijcia','icann','iconip','talip','aamas','kbs','ai')
		group by normalized_venue order by normalized_venue desc)
		to '/Users/admin/Desktop/data/dblp_trust_rep/data/conferences_first_publication_year.csv'
		with DELIMITER ',' CSV HEADER QUOTE '"';