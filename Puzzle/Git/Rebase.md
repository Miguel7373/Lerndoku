git co main   
git pull     
git co - 
git rebase origin/main 
git rebase --continue (only if you had merge conflicts)
git push --force-with-lease  


Bei einem Rebase werden die Commits eines Branches auf die Spitze eines anderen Branches verschoben, sodass sie so aussehen, als wären sie direkt darauf entstanden.
![[Pasted image 20240822084258.png]]