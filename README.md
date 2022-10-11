# lnproxy-cli

[check-wrap.py](check-wrap.py)
is a no-dependencies python script that
takes two invoices and makes sure that their payment hashes match.

## Example usage:

Adapted from [raspiblitz[(https://github.com/openoms/raspiblitz/blob/3875539468831342a9adeed52d4337af0dcec8ab/home.admin/_commands.sh#L456):

```
function lnproxy() {
  if [ $(cat /mnt/hdd/raspiblitz.conf 2>/dev/null | grep -c "runBehindTor=on") -eq 1 ]; then
    echo
    echo "Requesting a wrapped invoice from rdq6tvulanl7aqtupmoboyk2z3suzkdwurejwyjyjf4itr3zhxrm2lad.onion ..."
    echo
    wrapped=`torify curl http://rdq6tvulanl7aqtupmoboyk2z3suzkdwurejwyjyjf4itr3zhxrm2lad.onion/api/${1}`
    check-wrap.py $1 $wrapped
    echo $wrapped
  else
    echo
    echo "Requesting a wrapped invoice from https://lnproxy.org ..."
    echo
    wrapped=`curl https://lnproxy.org/api/${1}`
    check-wrap.py $1 $wrapped
    echo $wrapped
  fi
}
```
