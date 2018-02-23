# [Dedupe](https://github.com/dedupeio/dedupe), a library that uses machine learning to perform de-duplication and entity resolution quickly on structured data.

Install all prerequisite libraries:
I used python 2.7 
```bash
pip install -r requirements.txt
```

Run and find duplictes in input record:
```bash
python record_deduplication.py
```
  (use 'y', 'n' and 'u' keys to flag duplicates for active learning, 'f' when you are finished)

## Training

The training of algorithm is through human input. In order to figure out the best rules to deduplicate a set of data, you must give it a set of labeled examples to learn from.

The more labeled examples you give it, the better the deduplication results will be. At minimum, you should try to provide 10 positive matches and 10 negative matches.

The results of your training will be saved in a JSON file (file_training.json) for future runs of dedupe.
Delete the file_training.json if you wants to re-train the model.

Here's an example labeling operation:

```bash
ln :  SMITH JR
dob :  01-03-68
gn :  F
fn :  WILLIAM

ln :  ROTHMEYER JR
dob :  01-03-68
gn :  F
fn :  WILLIAM

Do these records refer to the same thing?
(y)es / (n)o / (u)nsure / (f)inished
```

Note: usually Bill is nickname for William. Similarly Bob is nickname for Robert.
Jack from John, Chuck from Charles, Peggy from Margret, Ted from Edword, Harry or Hank from Henry, 
Jim from James, Sally from Sarah, Dick for Richard, 
Source: https://thechive.com/2017/01/24/12-surprisingly-cool-origins-of-common-nicknames/

Outpt is stored into file_output.csv
Sort the content of file_output.csv based upon column Cluster ID.
Description of columns of file_output.csv:
	Cluster ID: Id of a cluster of duplicate records
	confidence_score: confidence of the element being in that cluster.
	Id: TO uniqually identify each row of input file.
	ln: Same as input file (last name)
	dob: Same as input file (date of birth)
	gn: Same as input file (gender)
	fn: Same as input file (first name)
	canonical_ln: Combined ln 
	canonical_dob: Combined dob
	canonical_Id: Combined Id
	canonical_fn: Combined fn
	canonical_gn: Combined gn
