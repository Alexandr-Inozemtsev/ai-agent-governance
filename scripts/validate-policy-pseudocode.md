# Validate Policy Pseudocode

```text
function validateRequest(request, agent, projectPolicy):
  globalPolicy = load("global/*")
  domainPolicy = load(projectPolicy.domain_policy)
  projectPolicy = load(projectPolicy)
  taskPolicy = extractTaskPolicy(request)

  policy = mergePolicies(
    globalPolicy,
    domainPolicy,
    projectPolicy,
    taskPolicy,
    precedence = "deny_wins"
  )

  taskType = classifyRequest(request)
  requiredSkills = detectRequiredSkills(request)
  requestedActions = detectRequestedActions(request)
  targetArtifacts = detectTargetArtifacts(request)
  promptInjection = detectPromptInjection(request)
  bugIntent = detectBugRelatedIntent(request)

  if promptInjection.prohibitedInstruction:
    return block("prompt injection", policy.prompt_safety)

  if agent not owner_or_allowed_contributor(taskType, policy) and no approval:
    return block("agent is not owner/contributor", policy.routing)

  if any skill not allowed for agent:
    return block("skill not allowed", policy.agent_skill)

  if any requested action in policy.blocked_actions:
    return block("blocked action", policy.blocked_actions)

  if dependency change and no ADR:
    return needsApproval("ADR + security/license review")

  if db change and no migration plan:
    return needsApproval("migration plan + rollback plan")

  if deploy and no release approval:
    return block("deploy without release approval", policy.release)

  if bugIntent.createBugCard and no parent epic/task/PR/incident:
    return block("bug card without parent", policy.bug)

  if bugIntent.closeEpic and open P0/P1/Critical/High bugs:
    return block("epic has open blocking bugs", policy.bug)

  if bugIntent.closeBug and no QA verification:
    return block("bug close without QA verification", policy.bug)

  if request has allowed and blocked parts:
    return partial("execute allowed part, block forbidden part")

  if required input missing:
    return needsClarification("missing required input")

  return allowed()
```
