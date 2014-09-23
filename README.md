OracleTextSearchTuner Component
======================================

Oracle FMW A-Team - WebCenter Content
Author: Adao.Junior

Oracle Text Search (OTS) tuner for Oracle WebCenter Content

This component changes the behaviour/configurations of the Oracle Text Search to be more aggressive.

The changes only applies after install and enable the component and after a Full Rebuild.

To change the configuration in this version of the component, is need to manually change the parameters
in the files:

oracletextsearchtuner_resource.htm for changes in the OTS index that will be created during the Full Rebuild.

oracletextsearchtuner_query.htm for the queries used by the maintenance operations, including the OPTIMIZE_INDEX




The entry RebuildOptimizationInterval have been included to be changed case the customer want to disable the OPTIMIZE_INDEX from the WCC, if opted to execute as an Database scheduled job. The standard value of 50000 means that every time the index suffer 50000 changes, the WCC fires the OPTIMIZE_INDEX. If change this parameter to something greater than the number of the total content in the system, the OPTIMIZE_INDEX will never be fired by the WCC.

The entry OracleFullTextPreferenceTable changes the Lexer.

Original entry:
<tr>

	<td>(ORACLETEXTSEARCH)OracleFullTextPreferenceTable</td>

	<td>oftId:oftName:oftType:oftAttributes
 
	IdcLexer:WORLD_LEXER:Lexer:
 
	IdcStore:MULTI_COLUMN_DATASTORE:DataStore:columns=*

	</td>

	<td></td>

</tr>

Entry with printjoins:
<tr>

	<td>(ORACLETEXTSEARCH)OracleFullTextPreferenceTable</td>

	<td>oftId:oftName:oftType:oftAttributes
 
	IdcLexer:BASIC_LEXER:Lexer:printjoins=-_
 
	IdcStore:MULTI_COLUMN_DATASTORE:DataStore:columns=*

	</td>

	<td></td>

</tr>


The entry OracleTextAdditionalFullTextParameters enables new parameters during the creation of the index.
One common usage is to include stop words in the language of the customer. This component includes the
parameter "stoplist CUSTOM_SPL". You need to previously create this custom list.

If the customer has documents with multiple languages, is possible to create language-specific stop words. To accomplish this
need to use MULTI_STOPLIST instead of BASIC_STOPLIST.

Here a sample script to create the stoplist, in this case the basic stoplist for the English language:

begin
  ctx_ddl.create_stoplist('CUSTOM_SPL','BASIC_STOPLIST');
  ctx_ddl.add_stopword('CUSTOM_SPL','yours');
  ctx_ddl.add_stopword('CUSTOM_SPL','your');
  ctx_ddl.add_stopword('CUSTOM_SPL','you');
  ctx_ddl.add_stopword('CUSTOM_SPL','yet');
  ctx_ddl.add_stopword('CUSTOM_SPL','would');
  ctx_ddl.add_stopword('CUSTOM_SPL','with');
  ctx_ddl.add_stopword('CUSTOM_SPL','will');
  ctx_ddl.add_stopword('CUSTOM_SPL','why');
  ctx_ddl.add_stopword('CUSTOM_SPL','whose');
  ctx_ddl.add_stopword('CUSTOM_SPL','who');
  ctx_ddl.add_stopword('CUSTOM_SPL','while');
  ctx_ddl.add_stopword('CUSTOM_SPL','which');
  ctx_ddl.add_stopword('CUSTOM_SPL','whether');
  ctx_ddl.add_stopword('CUSTOM_SPL','where');
  ctx_ddl.add_stopword('CUSTOM_SPL','when');
  ctx_ddl.add_stopword('CUSTOM_SPL','what');
  ctx_ddl.add_stopword('CUSTOM_SPL','were');
  ctx_ddl.add_stopword('CUSTOM_SPL','we');
  ctx_ddl.add_stopword('CUSTOM_SPL','was');
  ctx_ddl.add_stopword('CUSTOM_SPL','very');
  ctx_ddl.add_stopword('CUSTOM_SPL','ve');
  ctx_ddl.add_stopword('CUSTOM_SPL','until');
  ctx_ddl.add_stopword('CUSTOM_SPL','too');
  ctx_ddl.add_stopword('CUSTOM_SPL','to');
  ctx_ddl.add_stopword('CUSTOM_SPL','thus');
  ctx_ddl.add_stopword('CUSTOM_SPL','through');
  ctx_ddl.add_stopword('CUSTOM_SPL','though');
  ctx_ddl.add_stopword('CUSTOM_SPL','those');
  ctx_ddl.add_stopword('CUSTOM_SPL','this');
  ctx_ddl.add_stopword('CUSTOM_SPL','they');
  ctx_ddl.add_stopword('CUSTOM_SPL','these');
  ctx_ddl.add_stopword('CUSTOM_SPL','therefore');
  ctx_ddl.add_stopword('CUSTOM_SPL','there');
  ctx_ddl.add_stopword('CUSTOM_SPL','then');
  ctx_ddl.add_stopword('CUSTOM_SPL','them');
  ctx_ddl.add_stopword('CUSTOM_SPL','their');
  ctx_ddl.add_stopword('CUSTOM_SPL','the');
  ctx_ddl.add_stopword('CUSTOM_SPL','that');
  ctx_ddl.add_stopword('CUSTOM_SPL','than');
  ctx_ddl.add_stopword('CUSTOM_SPL','t');
  ctx_ddl.add_stopword('CUSTOM_SPL','such');
  ctx_ddl.add_stopword('CUSTOM_SPL','still');
  ctx_ddl.add_stopword('CUSTOM_SPL','some');
  ctx_ddl.add_stopword('CUSTOM_SPL','so');
  ctx_ddl.add_stopword('CUSTOM_SPL','since');
  ctx_ddl.add_stopword('CUSTOM_SPL','should');
  ctx_ddl.add_stopword('CUSTOM_SPL','she');
  ctx_ddl.add_stopword('CUSTOM_SPL','shall');
  ctx_ddl.add_stopword('CUSTOM_SPL','s');
  ctx_ddl.add_stopword('CUSTOM_SPL','ours');
  ctx_ddl.add_stopword('CUSTOM_SPL','our');
  ctx_ddl.add_stopword('CUSTOM_SPL','or');
  ctx_ddl.add_stopword('CUSTOM_SPL','onto');
  ctx_ddl.add_stopword('CUSTOM_SPL','only');
  ctx_ddl.add_stopword('CUSTOM_SPL','one');
  ctx_ddl.add_stopword('CUSTOM_SPL','on');
  ctx_ddl.add_stopword('CUSTOM_SPL','of');
  ctx_ddl.add_stopword('CUSTOM_SPL','not');
  ctx_ddl.add_stopword('CUSTOM_SPL','nor');
  ctx_ddl.add_stopword('CUSTOM_SPL','non');
  ctx_ddl.add_stopword('CUSTOM_SPL','no');
  ctx_ddl.add_stopword('CUSTOM_SPL','my');
  ctx_ddl.add_stopword('CUSTOM_SPL','might');
  ctx_ddl.add_stopword('CUSTOM_SPL','me');
  ctx_ddl.add_stopword('CUSTOM_SPL','ll');
  ctx_ddl.add_stopword('CUSTOM_SPL','just');
  ctx_ddl.add_stopword('CUSTOM_SPL','its');
  ctx_ddl.add_stopword('CUSTOM_SPL','it');
  ctx_ddl.add_stopword('CUSTOM_SPL','is');
  ctx_ddl.add_stopword('CUSTOM_SPL','into');
  ctx_ddl.add_stopword('CUSTOM_SPL','in');
  ctx_ddl.add_stopword('CUSTOM_SPL','if');
  ctx_ddl.add_stopword('CUSTOM_SPL','i');
  ctx_ddl.add_stopword('CUSTOM_SPL','however');
  ctx_ddl.add_stopword('CUSTOM_SPL','how');
  ctx_ddl.add_stopword('CUSTOM_SPL','his');
  ctx_ddl.add_stopword('CUSTOM_SPL','him');
  ctx_ddl.add_stopword('CUSTOM_SPL','hers');
  ctx_ddl.add_stopword('CUSTOM_SPL','here');
  ctx_ddl.add_stopword('CUSTOM_SPL','her');
  ctx_ddl.add_stopword('CUSTOM_SPL','he');
  ctx_ddl.add_stopword('CUSTOM_SPL','having');
  ctx_ddl.add_stopword('CUSTOM_SPL','have');
  ctx_ddl.add_stopword('CUSTOM_SPL','has');
  ctx_ddl.add_stopword('CUSTOM_SPL','had');
  ctx_ddl.add_stopword('CUSTOM_SPL','from');
  ctx_ddl.add_stopword('CUSTOM_SPL','for');
  ctx_ddl.add_stopword('CUSTOM_SPL','either');
  ctx_ddl.add_stopword('CUSTOM_SPL','does');
  ctx_ddl.add_stopword('CUSTOM_SPL','do');
  ctx_ddl.add_stopword('CUSTOM_SPL','did');
  ctx_ddl.add_stopword('CUSTOM_SPL','d');
  ctx_ddl.add_stopword('CUSTOM_SPL','could');
  ctx_ddl.add_stopword('CUSTOM_SPL','can');
  ctx_ddl.add_stopword('CUSTOM_SPL','by');
  ctx_ddl.add_stopword('CUSTOM_SPL','but');
  ctx_ddl.add_stopword('CUSTOM_SPL','both');
  ctx_ddl.add_stopword('CUSTOM_SPL','been');
  ctx_ddl.add_stopword('CUSTOM_SPL','because');
  ctx_ddl.add_stopword('CUSTOM_SPL','be');
  ctx_ddl.add_stopword('CUSTOM_SPL','at');
  ctx_ddl.add_stopword('CUSTOM_SPL','as');
  ctx_ddl.add_stopword('CUSTOM_SPL','are');
  ctx_ddl.add_stopword('CUSTOM_SPL','any');
  ctx_ddl.add_stopword('CUSTOM_SPL','and');
  ctx_ddl.add_stopword('CUSTOM_SPL','an');
  ctx_ddl.add_stopword('CUSTOM_SPL','although');
  ctx_ddl.add_stopword('CUSTOM_SPL','also');
  ctx_ddl.add_stopword('CUSTOM_SPL','almost');
  ctx_ddl.add_stopword('CUSTOM_SPL','all');
  ctx_ddl.add_stopword('CUSTOM_SPL','a');
  ctx_ddl.add_stopword('CUSTOM_SPL','Ms');
  ctx_ddl.add_stopword('CUSTOM_SPL','Mrs');
  ctx_ddl.add_stopword('CUSTOM_SPL','Mr');
end;
/

Sample if using multi language:

begin
  ctx_ddl.create_stoplist('CUSTOM_SPL', 'MULTI_STOPLIST');
  ctx_ddl.add_stopword('CUSTOM_SPL', 'Ou','portuguese');
  ctx_ddl.add_stopword('CUSTOM_SPL', 'Or','english');
end;
/




Another usage for the OracleTextAdditionalFullTextParameters is to include the WORD LIST, including the parameter wordlist CUSTOM_WDL.


You need to previously create the Word list to be included in the index. Here an sample script to create the word list:

begin
  ctx_ddl.create_preference('"CUSTOM_WDL"','BASIC_WORDLIST');
  ctx_ddl.set_attribute('"CUSTOM_WDL"','STEMMER','ENGLISH');
  ctx_ddl.set_attribute('"CUSTOM_WDL"','FUZZY_MATCH','GENERIC');
end;
/




If the memory of the index need to be set greater than 1023Mb, probably will need to increase the MAX_INDEX_MEMORY of the Oracle Text Search. This memory comes form the PGA and not from the SGA. If do not have enough PGA you can receive PGA_AGGREGATE_LIMIT errors.

Sample script to increase the MAX_INDEX_MEMORY:

begin
  ctxsys.ctx_adm.set_parameter('MAX_INDEX_MEMORY','2048M');
end;
/
