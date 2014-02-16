# p:otherwise

In XProc v1, `p:otherwise` is the required last child of `p:choose`.
In XProc v2, it could be optional.

All the subpipelines in the `p:when`/`p:otherwise` children of
`p:choose` are required to declare the same output ports.

If there is no `p:otherwise` declared and none of the `p:when`
tests succeed; then the primary output port (if declared) can be connected
to the default readable port, and all other ports can  output
empty sequences (as if connected to `p:empty`).
