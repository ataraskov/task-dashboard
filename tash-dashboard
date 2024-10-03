#!/bin/sh

MY_LOCATION="$(dirname "$0")"
#export TASKRC="$MY_LOCATION/.taskrc"
#export TASKDATA="$MY_LOCATION/.task"
SESSION="tasks-dashboard"
SESSIONEXISTS=$(tmux list-sessions | grep $SESSION)

if [ "$SESSIONEXISTS" = "" ]
then
  tmux new -s $SESSION -n view -d bash
  tmux set -t $SESSION:view status off
  tmux split-window -t $SESSION:view.0 -v -l 2  bash
  tmux split-window -t $SESSION:view.0 -v -l 60% bash
  tmux split-window -t $SESSION:view.0 -h -l 40% bash
  tmux split-window -t $SESSION:view.2 -h -l 40% bash
  tmux send-keys    -t $SESSION:view.0 'watch -c "task rc.verbose:label rc.hooks:off rc._forcecolor:on"' 'C-m'
  tmux select-pane  -t $SESSION:view.1
  tmux send-keys    -t $SESSION:view.1 'EDITOR=vim task shell' 'C-m'
  tmux send-keys    -t $SESSION:view.2 'while task rc.hooks:off burndown.daily; do sleep 30; done' 'C-m'
  tmux send-keys    -t $SESSION:view.3 'watch -t -c "task rc.verbose:label rc.hooks:off rc.context:none rc._forcecolor:on summary; task history"' 'C-m'
  tmux send-keys    -t $SESSION:view.4 'watch -t -c "echo \"# active\";task rc.verbose:label rc.hooks:off rc.context:default rc._forcecolor:on active; echo; echo \"# overdue\"; task rc.verbose:label rc.hooks:off rc.context:default overdue"' 'C-m'
fi

tmux attach-session -t $SESSION
